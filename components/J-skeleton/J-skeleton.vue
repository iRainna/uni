<template>
	<view>
		<view v-if="loading" class="skeleton" :class="{ animate: animate }" :style="{ justifyContent: flexType }">
			<!-- 轮播图 -->
			<view v-if="imgTitle" class="skeleton-imgTitle" style="width:100%;border-radius: 10px;height: 360rpx;display: block;"></view>
			<!-- 头像图 -->

			<view
				v-if="showAvatar && !imgTitle"
				class="skeleton-avatar"
				v-for="(item, index) in nameRow"
				:key="index"
				:class="[avatarShape]"
				:style="{ width: avatarSize, height: avatarSizea }"
			></view>
			<!-- 文字条 -->
			<view class="skeleton-content" v-if="showTitle && !imgTitle">
				<view class="skeleton-title" :style="{ width: titleWidth }"></view>
				<view class="skeleton-rows"><view class="skeleton-row-item" v-for="(item, index) in rowList" :key="index" :style="{ width: item.width }"></view></view>
			</view>

			<!-- 动态 -->
			<view class="skeleton-content dong_top" v-if="showDong && !imgTitle">
				
				<view class="dong_right">
					<view class="dong_head float">
						<view class="dong_left "></view>
						<view class="dong_you"></view>
					</view>
					<view class="dong_xing"></view>
				</view>
			</view>
		</view>
		<view v-else><slot></slot></view>
	</view>
</template>

<script>
const DEFAULT_ROW_WIDTH = '100%';
const DEFAULT_LAST_ROW_WIDTH = '60%';

export default {
	props: {
		loading: {
			type: Boolean,
			default: true
		},
		imgTitle: {
			type: Boolean,
			default: false
		},
		nameRow: {
			type: Number,
			default: 1
		},
		flexType: {
			type: String,
			default: 'flex-start' // center	居中	√		space-between	两端对齐	√		space-around	子元素拉手分布	√		flex-start	居左		flex-end	居右
		},
		showAvatar: {
			type: Boolean,
			default: true
		},
		avatarSize: {
			type: String,
			default: '50px'
		},
		avatarSizea: {
			type: String,
			default: '50px'
		},
		avatarShape: {
			type: String,
			default: 'round' // square | round
		},
		showTitle: {
			type: Boolean,
			default: false
		},
		titleWidth: {
			type: String,
			default: '40%'
		},
		row: {
			type: Number,
			default: 3
		},
		animate: {
			type: Boolean,
			default: true
		},
		showDong: {
			type: Boolean,
			default: false
		}
	},
	data() {
		return {};
	},
	computed: {
		rowList() {
			let list = [];
			for (let i = 0; i < this.row; i++) {
				list.push({
					width: i === this.row - 1 && i !== 0 ? DEFAULT_LAST_ROW_WIDTH : DEFAULT_ROW_WIDTH
				});
			}
			return list;
		}
	}
};
</script>

<style scoped>
.skeleton {
	display: flex;
	--bg-color: #f2f3f5;
	--row-height: 16px;
	--row-margin-top: 16rpx;
}
.skeleton-imgTitle {
	flex-wrap: wrap;
	background: var(--bg-color);
	margin: 10px auto;
}
.skeleton-avatar {
	flex-shrink: 0;
	background: var(--bg-color);
	margin-right: 8px;
}
.skeleton-avatar.round {
	border-radius: 50%;
}

.skeleton-content {
	width: 100%;
}

.skeleton-title {
	background-color: var(--bg-color);
	height: var(--row-height);
}

.skeleton-title + .skeleton-rows {
	margin-top: var(--row-margin-top);
}

.skeleton-rows {
}

.skeleton-row-item {
	background-color: var(--bg-color);
	height: var(--row-height);
}
.skeleton-row-item:not(:first-child) {
	margin-top: var(--row-margin-top);
}

.skeleton.animate {
	animation: skeleton-blink 1.2s ease-in-out infinite;
}

.dong_top {
	overflow: hidden;
	display: flex;
}
.dong_img {
	display: block;
	width: 90rpx;
	height: 90rpx;
	border-radius: 50%;
	display: none;
}

.dong_right {
	overflow: hidden;
	width: 100%;

}
.dong_head {
	overflow: hidden;
	display: flex;
		margin-top: 10rpx;
	
}
.dong_left {
	overflow: hidden;
	width: 220rpx;
	background-color: var(--bg-color);
	height: var(--row-height);
}

.dong_you {
	overflow: hidden;
	width: 115rpx;
	background-color: var(--bg-color);
	height: var(--row-height);
}

.dong_xing {
	overflow: hidden;
	width: 100%;
	background-color: var(--bg-color);
	height: var(--row-height);
	margin-top: 15rpx;
}

@keyframes skeleton-blink {
	0% {
		opacity: 1;
	}
	50% {
		opacity: 0.6;
	}
	100% {
		opacity: 1;
	}
}
</style>

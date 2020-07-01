<template>
	<view class="starTop">
		 <view class="star_fg zhong center">
		 <image src="../../static/image/default.png"></image>
		 </view>
		<!-- 跳过 -->
		<image src="../../static/tiaoa.gif" class="tiao" mode="" @click="login()"></image>
	</view>
</template>

<script>
export default {
	data() {
		return {
			timer: null
		};
	},
	onLoad() {
		this.timer = setTimeout(function() {
			uni.navigateTo({
				url: '/pages/index/login/login'
			});
		}, 250000);
	},
	methods: {
		login() {
			if (this.timer) {
				clearTimeout(this.timer);
			}
			uni.navigateTo({
				url: '/pages/index/login/login'
			});
		}
	}
};
</script>

<style>

.star_fg image{
	display: block;
	width:312rpx;
	height: 82rpx;
	margin: 0 auto;
}

.star_fg{
	overflow: hidden;
	display: flex;
	position: fixed;
	left: 0;
	width: 100%;
	bottom: 60rpx;
	margin-bottom: 0;
	z-index: 10;
}	
	
.starTop image.tiao {
	width: 70rpx !important;
	height: 70rpx !important;
	display: block;
	overflow: hidden;
	position: absolute;
	right: 1em;
	top: 2em;
	z-index: 10;
}

.starTop {
	width: 100%;
	height: 100%;
	overflow: hidden;
	position: relative;
}

page {
	width: 100%;
	height: 100%;
	overflow: hidden;
}
</style>

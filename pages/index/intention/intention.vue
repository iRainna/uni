<template>
	<view class="duanWang">
		<view class="duanWang inte_footer">
			<view class="inte_nei">
				<view class="inte_text">可选择1个考试随时可重选</view>
				<view class="inte_list">
					<view class="inte_li" v-for="(item, index) in list" :key='index'>
						<view class="inte_title">{{ item.title }}</view>
						<view class="inte_dl">
							<view class="inte_dd zhong center" v-for="(itemChild, indexChild) in item.child" :class="item.isTab== indexChild?'on':''" @click="tabClick(item,indexChild)" :key='indexChild'>
								<text>{{ itemChild.text }}</text>
							</view>
						</view>
					</view>
				</view>
				<!-- 上拉加载更多图标和文字-->
				<load-more :showLoadMore="isMore" :isNoLoad="isNoLoad" :loadMoreText="loadMoreText"></load-more>
			</view>
			<!-- 暂无数据 -->
			<no-data :isNoText="isNoText" :nodata="list.length == 0"></no-data>
		</view>
		<!-- 01 -->
		<view class="footer"><view class="footer_btn" :class="isXuan?'on':''" @click="homeClick()">选好了</view></view>
	</view>
</template>

<script>
import loadMore from '@/components/more/more.vue';
import noData from '@/components/noData/noData.vue';
export default {
	data() {
		return {
			isNodata: false, //是否显示暂无数据
			isNoLoad: true,
			isNoText: '暂无数据~',
			// 按钮
			isXuan:true,
			// 上拉
			list: [],
			isMore: false,
			loadMoreText: '加载中...',
			showLoadMore: false,
			max: 0,
			
		};
	},
	components: {
		loadMore,
		noData
	},
	onLoad() {
		this.initData();
	},
	onUnload() {
		(this.max = 0), (this.list = []), (this.loadMoreText = '加载更多'), (this.showLoadMore = false);
	},
	onReachBottom() {
		console.log('onReachBottom');
		if (this.max > 40) {
			this.loadMoreText = '没有更多数据了!';
			return;
		}
		this.showLoadMore = true;
		setTimeout(() => {
			this.setDate();
		}, 300);
	},
	onPullDownRefresh() {
		console.log('onPullDownRefresh');
		this.initData();
	},
	methods: {
		initData() {
			setTimeout(() => {
				this.max = 0;
				this.list = [];
				let list = [];
				this.max += 10;
				for (var i = this.max - 9; i < this.max + 1; i++) {
					list.push({
						title: '建工类',
						isTab:-1,
						child: [
							{
								text: '一级工程实训网'
							},
							{
								text: '一级工程实训网'
							},
							{
								text: '一级工程实训网'
							},
							{
								text: '一级工程实训网'
							},
							{
								text: '一级工程实训网'
							}
						]
					});
				}
				this.list = this.list.concat(list);
				uni.stopPullDownRefresh();
			}, 300);
		},
		setDate() {
			let list = [];
			this.max += 10;
			for (var i = this.max - 9; i < this.max + 1; i++) {
				list.push({
					title: '建工类',
					isTab:-1,
					child: [
						{
							text: '一级工程实训网'
						},
						{
							text: '一级工程实训网'
						},
						{
							text: '一级工程实训网'
						},
						{
							text: '一级工程实训网'
						},
						{
							text: '一级工程实训网'
						}
					]
				});
			}
			this.list = this.list.concat(list);
		},
		tabClick(item,index){
			item.isTab = index 
			this.isXuan = false
		},
		// homeClick
		homeClick(){
			uni.switchTab({
				url:'/pages/home/home'
			})
		}
	}
};
</script>

<style>

.footer_btn.on{
	background: #b3b3b3 !important;
}

.inte_dd.on{
	background-color: #fce9e9;
	border: solid 1rpx #e5252a;
	box-sizing: border-box;
}	


.inte_dd.on text{
		color: #e5252a;
}

.inte_footer{
	padding-bottom: 128rpx;
}
	
.footer_btn {
	overflow: hidden;
	width: 92%;
	height: 88rpx;
	line-height: 88rpx;
	border-radius: 10rpx;
	margin: 0 auto;
	font-size: 28rpx;
	color: #fff;
	text-align: center;
	background: linear-gradient(to right, #e93237, #fa7276) !important; /* 标准的语法 */
}

.footer {
	overflow: visible;
	width: 100%;
	-moz-box-shadow: 0px -2px 5px #e9e9eb;
	-webkit-box-shadow: 0px -2px 5px #e9e9eb;
	box-shadow: 0px -2px 5px #e9e9eb;
	position: fixed;
	left: 0;
	bottom: 0;
	z-index: 10;
	padding-top: 20rpx;
	padding-bottom: 20rpx;
	background-color: #fff;
}

/* footer */

.inte_dd text {
	font-size: 24rpx;
	color: #333;
	display: block;
	padding-left: 20rpx;
	padding-right: 20rpx;
	text-align: center;
	display: -webkit-box;
	-webkit-box-orient: vertical;
	-webkit-line-clamp: 2;
	overflow: hidden;
}

.inte_dd {
	width: 160rpx;
	height: 90rpx;
	background-color: #f5f7fb;
	border-radius: 4rpx;
	display: flex;
	float: left;
	margin-right: 16rpx;
	margin-bottom: 20rpx;
	border: solid 1rpx #fff;
	box-sizing: border-box;
}

.inte_dd:nth-child(4n + 4) {
	margin-right: 0;
}

.inte_dl {
	overflow: hidden;
	margin-top: 30rpx;
}

.inte_title {
	overflow: hidden;
	font-size: 28rpx;
	color: #333;
	font-weight: 600;
}

.inte_li {
	overflow: hidden;
	margin-top: 60rpx;
}

.inte_list {
	overflow: hidden;
}

/* inte_list */

.inte_text {
	font-size: 24rpx;
	color: #999;
	text-align: center;
	padding-top: 40rpx;
}

.inte_nei {
	overflow: hidden;
	padding-left: 30rpx;
	padding-right: 30rpx;
}

.duanWang {
	border-top: solid 1rpx #eeeeee;
}
</style>

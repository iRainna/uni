<template>
	<view>
		<view v-if="!isDuanWang">
			<view v-if="!isNodata">
				<!-- 头部 -->
				<view class="shopCar-head">
					<view class="shopCar-head-img01" @click="goBack"><image src="../../../static/image/nav_Return.png"></image></view>
					<view class="shopCar-head-txt01">我的订单</view>
					<view class="shopCar-head-txt02">清空购物车</view>
				</view>
				<view class="shopCar-con">
					<view class="shopCar-list flex" v-for="(item,index) in listData" :key='index'>
						<view class="shopCar-list-rad" @click="selBtn(index)">
							<image :src="item.bOn?'../../../static/image/Single_a.png':'../../../static/image/Single_aa.png'"></image>
						</view>
						<view class="shopCar-list-c01">
							<view class="shopCar-lic-txt01">{{item.name}}</view>
							<view class="flex flex-sb zhong">
								<view class="flex zhong">
									<text class="shopCar-cprice01">￥{{item.price1}}</text>
									<text class="shopCar-cprice02">原价￥{{item.price2}}</text>
								</view>
								<view class="flex zhong">
									<view class="flex zhong">
										<view class="cli-cimg01" @click="subtract()">
											<image src="../../../static/image/shop_reduce.png"></image>
										</view>
										<view class="cli-ctxt01">{{count}}</view>
										<view class="cli-cimg01" @click="add()">
											<image src="../../../static/image/shop_plus.png"></image>
										</view>
									</view>
									<view class="cli-cimg02">
										<image src="../../../static/image/del_icon02.png"></image>
									</view>
								</view>
							</view>
						</view>
					</view>
					<!-- 上拉加载 -->
					<on-more :showLoadMore="isMore" :loadMoreText="loadMoreText"></on-more>
				</view>
				<view class="shopCar-btn flex flex-sb">
					<view class="flex shopCar-btn-left" @click="allBtn">
						<view class="shopCar-all">
							<image :src="all?'../../../static/image/Single_a.png':'../../../static/image/Single_aa.png'"></image>
						</view>
						<text class="shopCar-txt01">全选</text>
					</view>
					<view class="flex shopCat-btn-right">
						<view class="shopCar-btn-con">
							<view class="flex">
								<text class="shopCar-btn-c01">合计</text>
								<text class="shopCar-btn-c02">(不含运费):</text>
								<text class="shopCar-btn-c03">￥199.00</text>
							</view>
							<view class="shopCar-btn-ctxt01">已选件数1件,已节省:￥190</view>
						</view>
						<button class="shopCar-con-btn">去结算</button>
					</view>
				</view>
			</view>
			<!-- 暂无数据 -->
			<no-data :isNoText="isNoText" :nodata="isNodata" v-else></no-data>
		</view>
		<!-- 断网 -->
		<duan-wang :duanWang="isDuanWang"></duan-wang>
	</view>
</template>

<script>
	import duanWang from '@/components/duanWang/duanWang.vue';
	import noData from '@/components/noData/noData.vue';
	import onMore from '@/components/more/more.vue';
	export default {
		components:{
			duanWang,
			noData,
			onMore
		},
		data() {
			return {
				/* 上拉加载 */
				isMore: true,
				loadMoreText: '加载中...',
				// 断网：
				isDuanWang: false,
				/* 判断是否有数据 */
				isNodata:false,
				isNoText: '-你的购物车里面还是空的哦-',
				count: 1,
				listData:[],
				/* 全选 */
				all:false
			}
		},
		methods: {
			allBtn(index){
				this.all = !this.all
			},
			/* 多选 */
			selBtn: function(index){
				this.list[index].bOn = !this.list[index].bOn;
			},
			/* 返回上一级 */
			goBack(){
				uni.navigateBack({
					delta:1
				})
			},
			add: function (count) {
				this.count++
			},
			subtract: function (count) {
				if (this.count <= 0) {
					alert('受不了啦，宝贝不能再减少啦')
					this.count = 0
				} else {
					this.count -= 1
				}
			},
			initData() {
				setTimeout(() => {
					this.max = 0;
					this.listData = [];
					let listData = [];
					this.max += 10;
					for (var i = this.max - 9; i < this.max + 1; i++) {
						listData.push({
						name:'课程名称课程名称课程名称课程名称课程名称课程名称',
						price1:'40',
						price2:'50',
						bOn:false,
					});
					}
					this.listData = this.listData.concat(listData);
					uni.stopPullDownRefresh();
				}, 300);
			},
			setDate() {
				let listData = [];
				this.max += 10;
				for (var i = this.max - 9; i < this.max + 1; i++) {
					listData.push({
						name:'课程名称课程名称课程名称课程名称课程名称课程名称',
						price1:'40',
						price2:'50',
						bOn:false,
					});
				}
				this.listData = this.listData.concat(listData);
			}
		},
		onLoad() {
			this.initData();
		},
		onUnload() {
			this.max = 0, this.listData = [], this.loadMoreText = '加载更多', this.showLoadMore = false;
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
		}
	}
</script>

<style>
page{
	background: #F7F7F7;
}
.shopCar-head{
	width: 100%;
	height: 88rpx;
	background: #fff;
	display: flex;
	align-items: center;
	padding-top: 44rpx;
	position: fixed;
	top: 0;
	left: 0;
	z-index: 13;
}
.shopCar-head-img01{
	margin-left: 30rpx;
	width: 44rpx;
	height: 44rpx;
}
.shopCar-head-img01 > image{
	width: 100%;
	height: 100%;
	display: block;
}
.shopCar-head-txt01{
	flex: 1;
	text-align: center;
	font-size: 32rpx;
	color: #000000;
}
.shopCar-head-txt02{
	margin-right: 30rpx;
	font-size: 28rpx;
	color: #9A9DA3;
}
.shopCar-con{
	margin: 162rpx auto 130rpx auto;
	padding: 0 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	overflow: hidden;
}
.shopCar-list{
	margin-bottom: 30rpx;
	padding: 40rpx 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	background: #fff;
	border-radius: 5rpx;
}
.shopCar-list-rad{
	width: 35rpx;
	height: 35rpx;
	margin-right: 30rpx;
}
.shopCar-list-rad image{
	width: 100%;
	height: 100%;
	display: block;
}
.shopCar-list-c01{
	flex: 1;
}
.shopCar-lic-txt01{
	padding-bottom: 30rpx;
	font-size: 28rpx;
	color: #0C101C;
}
.shopCar-cprice01{
	font-size: 30rpx;
	color: #E5252A;
	font-weight: bold;
}
.shopCar-cprice02{
	padding-left: 10rpx;
	font-size: 24rpx;
	text-decoration: line-through;
	color: #9A9DA3;
}
.cli-cimg01{
	width: 40rpx;
	height: 40rpx;
}
.cli-cimg01 image{
	width: 100%;
	height: 100%;
	display: block;
}
.cli-ctxt01{
	margin: 0 10rpx;
	width: 75rpx;
	height: 45rpx;
	text-align: center;
	line-height: 45rpx;
	background: #f2f2f2;
	border-radius: 5rpx;
	font-size: 26rpx;
	color: #0C101C;
}
.cli-cimg02{
	margin-left: 30rpx;
	width: 40rpx;
	height: 40rpx;
}
.cli-cimg02 image{
	width: 100%;
	height: 100%;
	display: block;
}
.shopCar-btn{
	padding:20rpx 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	background: #fff;
	position: fixed;
	bottom: 0;
	left: 0;
	box-shadow: 0 0 15px #ccc;
	justify-content: space-between;
}
.shopCar-btn-left{
	padding-top: 10rpx;
}
.shopCar-all{
	width: 35rpx;
	height: 35rpx;
	margin-right: 20rpx;
}
.shopCar-all image{
	width: 100%;
	height: 100%;
	display: block;
}
.shopCar-txt01{
	font-size: 28rpx;
	color: #0C101C;
}
.shopCat-btn-right{
	align-items: center;
}
.shopCar-btn-c01{
	font-size: 26rpx;
	color: #0C101C;
}
.shopCar-btn-c02{
	font-size: 24rpx;
	color: #9A9DA3;
}
.shopCar-btn-c03{
	font-size: 28rpx;
	color: #E5252A;
	font-weight: bold;
}
.shopCar-btn-ctxt01{
	padding-top: 10rpx;
	font-size: 24rpx;
	color: #9A9DA3;
}
.shopCar-con-btn{
	margin-left: 30rpx;
	width: 170rpx;
	height: 90rpx;
	line-height: 90rpx;
	text-align: center;
	border-radius: 10rpx;
	background-image: linear-gradient(to right,#e83035, #fa7276) !important;
	font-size: 28rpx;
	color: #fff;
}
</style>

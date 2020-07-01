<template>
	<view>
		<view v-if="!isDuanWang">
			<view class="my-head flex">
				<text>我的</text>
				<view class="my-head-img" @click="goSet">
					<image src="../../static/image/personal_setting.png"></image>
				</view>
			</view>
			<view class="my-content flex flex-sb">
				<view class="my-con01 flex">
					<view class="my-con-img">
						<image src="../../static/image/my_head.png"></image>
					</view>
					<view class="my-con-info">
						<text class="my-con-name">千小米</text>
						<text class="my-con-phone">12345644564</text>
					</view>
				</view>
				<view class="my-con02">
					<button class="my-con-btn" hover-class="none">签到</button>
					<text class="my-con-txt01">当前积分:20</text>
				</view>
			</view>
			
			<view class="my-center">
				<view class="my-center-c01 flex flex-sb" @click="goBalance">
					<view class="my-cent01 flex zhong">
						<image src="../../static/image/my_icon01.png"></image>
						<text>我的余额</text>
					</view>
					<view class="my-cent02 flex zhong">
						<text>100.00元</text>
						<image src="../../static/image/choose.png"></image>
					</view>
				</view>
				<view class="my-center-c01 flex flex-sb" @click="goOrder">
					<view class="my-cent01 flex zhong">
						<image src="../../static/image/my_icon04.png"></image>
						<text>我的订单</text>
					</view>
					<view class="my-cent02">
						<image src="../../static/image/choose.png"></image>
					</view>
				</view>
				<view class="my-center-c01 flex flex-sb" @click="goRemind">
					<view class="my-cent01 flex zhong">
						<image src="../../static/image/my_icon05.png"></image>
						<text>考试提醒</text>
					</view>
					<view class="my-cent02">
						<image src="../../static/image/choose.png"></image>
					</view>
				</view>
				<view class="my-center-c01 flex flex-sb" @click="goShopCar">
					<view class="my-cent01 flex zhong">
						<image src="../../static/image/my_icon06.png"></image>
						<text>购物车</text>
					</view>
					<view class="my-cent02">
						<image src="../../static/image/choose.png"></image>
					</view>
				</view>
				<view class="my-center-c01 flex flex-sb" @click="goAddress">
					<view class="my-cent01 flex zhong">
						<image src="../../static/image/addressa.png"></image>
						<text>地址管理</text>
					</view>
					<view class="my-cent02">
						<image src="../../static/image/choose.png"></image>
					</view>
				</view>
				<view class="my-center-c01 flex flex-sb" @click="goHelp">
					<view class="my-cent01 flex zhong">
						<image src="../../static/image/my_icon03.png"></image>
						<text>帮助中心</text>
					</view>
					<view class="my-cent02">
						<image src="../../static/image/choose.png"></image>
					</view>
				</view>
				<view class="my-center-c01 flex flex-sb" @click="goPromote">
					<view class="my-cent01 flex zhong">
						<image src="../../static/image/my_icon02.png"></image>
						<text>推广合作</text>
					</view>
					<view class="my-cent02">
						<image src="../../static/image/choose.png"></image>
					</view>
				</view>
			</view>
		</view>
		<!-- 断网 -->
		<duan-wang :duanWang="isDuanWang"></duan-wang>
	</view>
</template>

<script>
	import duanWang from '@/components/duanWang/duanWang.vue';
	export default {
		components:{
			duanWang
		},
		data() {
			return {
				// 断网：
				isDuanWang: false,
			}
		},
		methods: {
			/* 我的余额 */
			goBalance(){
				uni.navigateTo({
					url:'/pages/my/balance/balance'
				})
			},
			/* 我的订单 */
			goOrder(){
				uni.navigateTo({
					url:'/pages/my/order/order'
				})
			},
			/* 考试提醒 */
			goRemind(){
				uni.navigateTo({
					url:'/pages/my/remind/remind'
				})
			},
			/* 购物车 */
			goShopCar(){
				uni.navigateTo({
					url:'/pages/my/shopCar/shopCar'
				})
			},
			/* 地址管理 */
			goAddress(){
				uni.navigateTo({
					url:'/pages/my/address/address'
				})
			},
			/* 帮助中心 */
			goHelp(){
				uni.navigateTo({
					url:'/pages/my/help/help'
				})
			},
			/* 推广合作 */
			goPromote(){
				uni.navigateTo({
					url:'/pages/my/promote/promote'
				})
			},
			/* 设置 */
			goSet(){
				uni.navigateTo({
					url:'/pages/my/set/set'
				})
			}
		}
	}
</script>

<style>
page{
	background: #f7f7f7;
}
.my-head{
	padding-top: 44rpx;
	width: 100%;
	height: 88rpx;
	line-height: 88rpx;
	background: #fff;
	justify-content: flex-end;
	align-items: center;
	position: fixed;
	top: 0;
	left: 0;
	z-index: 13;
}
.my-head > text{
	width: calc( 100% - 74rpx );
	text-align: center;
	font-size: 32rpx;
	color: #1a1a1a;
}
.my-head-img{
	margin-right: 30rpx;
	width: 44rpx;
	height: 44rpx;
}
.my-head-img > image{
	width: 100%;
	height: 100%;
	display: block;
}
.my-content{
	margin-top: 132rpx;
	margin-bottom: 30rpx;
	padding: 0 30rpx;
	width: calc( 100% - 60rpx );
	height: 210rpx;
	background: #fff;
	align-items: center;
}
.my-con01{
	width: 360rpx;
	align-items: center;
}
.my-con-img{
	margin-right: 35rpx;
	width: 120rpx;
	height: 120rpx;
	background: url(../../static/image/personal_head.png)no-repeat;
	background-size: 100%;
	border-radius: 50%;
}
.my-con-img image{
	width: 100%;
	height: 100%;
	display: block;
	border-radius: 50%;
}
.my-con-info{
	width: calc( 100% - 155rpx );
}
.my-con-name{
	width: 100%;
	font-size: 34rpx;
	color: #1a1a1a;
	font-weight: bold;
}
.my-con-phone{
	width: 100%;
	font-size: 24rpx;
	color: #9a9da3;
}

.my-con-btn{
	width: 155rpx;
	height: 50rpx;
	line-height: 50rpx;
	border-radius: 50rpx;
	background-image: linear-gradient(to right, #e83136 , #f97074) !important;
	text-align: center;
	font-size: 26rpx;
	color: #fff;
}
.my-con-txt01{
	font-size: 24rpx;
	color: #9A9DA3;
	text-align: right;
}
.my-center{
	padding: 0 30rpx;
	width: calc( 100% - 60rpx);
	height: auto;
	overflow: hidden;
	background: #fff;
}
.my-center-c01{
	width: 100%;
	height: 110rpx;
	border-bottom: 1rpx solid #eee;
	align-items: center;
}
.my-center-c01:last-child{
	border-bottom: 0;
}
.my-cent01 image{
	width: 50rpx;
	height: 50rpx;
	display: block;
	margin-right: 25rpx;
}
.my-cent01 text{
	font-size: 28rpx;
	color: #000000;
}
.my-cent02 text{
	font-size: 24rpx;
	color: #9a9da3;
}
.my-cent02 image{
	margin-left: 20rpx;
	width: 11rpx;
	height: 24rpx;
}
</style>

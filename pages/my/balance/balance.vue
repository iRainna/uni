<template>
	<view>
		<view v-if="!isDuanWang">
			<view v-if="!isNodata" class="balance-con">
				<view class="balance-con-txt01">5000.00</view>
				<view class="balance-con-txt02">我的余额</view>
			</view>
			<!-- 暂无数据 -->
			<no-data :isNoText="isNoText" :nodata="isNodata" v-else></no-data>
			<button class="balance-btn" hover-class="none" @click="goPay">充值</button>
		</view>
		<!-- 断网 -->
		<duan-wang :duanWang="isDuanWang"></duan-wang>
	</view>
</template>

<script>
	import duanWang from '@/components/duanWang/duanWang.vue';
	import noData from '@/components/noData/noData.vue';
	export default {
		components:{
			duanWang,
			noData
		},
		data() {
			return {
				// 断网：
				isDuanWang: false,
				/* 判断是否有数据 */
				isNodata:false,
				isNoText: '-还没有余额哦！快去充值吧-',
			}
		},
		methods: {
			goPay(){
				uni.navigateTo({
					url:'/pages/my/balance_pay/balance_pay'
				})
			}
		}
	}
</script>

<style>
page{
	background: #F7F7F7;
}
.balance-con{
	margin:30rpx auto;
	width: 100%;
	height: 500rpx;
	background: #fff;
}
.balance-con-txt01{
	padding-top: 180rpx;
	width: 100%;
	text-align: center;
	font-size: 46rpx;
	color: #e5252a;
	font-weight: bold;
}
.balance-con-txt02{
	padding-top: 30rpx;
	width: 100%;
	font-size: 28rpx;
	color: #9a9da3;
	text-align: center;
}
.balance-btn{
	margin: 90rpx auto 0 auto;
	width: 93%;
	height: 90rpx;
	line-height: 90rpx;
	text-align: center;
	font-size: 28rpx;
	color: #fff;
	background-image: linear-gradient(to right, #07b666 , #22c67b) !important;
	border-radius: 10rpx;
}
</style>

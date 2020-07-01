<template>
	<view>
		<view v-if="!isDuanWang">
			<view class="pay-con01 flex flex-sb">
				<text class="pay-con-ctxt01">充值方式</text>
				<view class="pay-con-choose">
					<picker @change="bindPickerChange" :value="payType" :range="array">
						<view class="pay-choose-txt01">{{array[payType]}}</view>
					</picker>
					<image src="../../../static/image/choose.png"></image>
				</view>
			</view>
			<view class="pay-con02">
				<view class="pay-con02-txt01">充值金额</view>
				<view class="pay-con02-c01">
					<text class="pay-con-ctxt01">￥</text>
					<input class="pay-con-input" placeholder="请输入充值金额" />
				</view>
			</view>
			<button class="balance-btn" hover-class="none">充值</button>
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
				//支付方式
				array: ['微信', '支付宝'],
				payType: 0
			}
		},
		methods: {
			bindPickerChange: function(e) {
				this.payType = e.target.value
			},
			moveHandle(){}
		}
	}
</script>

<style>
page{
	background: #F7F7F7;
}
.pay-con01{
	margin: 30rpx auto;
	padding: 30rpx;
	width: calc( 100% - 60rpx );
	background: #fff;
	align-items: center;
}
.pay-con-ctxt01{
	font-size: 28rpx;
	color: #0c101c;
}
.pay-con-choose{
	align-items: center;
	display: flex;
}
.pay-con-choose .pay-choose-txt01{
	font-size: 28rpx;
	color: #0c101c;
}
.pay-con-choose > image{
	margin-left: 20rpx;
	width: 11rpx;
	height: 24rpx;
	display: block;
}
.pay-con02{
	padding: 30rpx;
	width: calc( 100% - 60rpx );
	height: 230rpx;
	background: #fff;
}
.pay-con02-txt01{
	padding: 30rpx 0;
	font-size: 28rpx;
	color: #0C101C;
}
.pay-con02-c01{
	padding: 20rpx 0;
	width: 100%;
	border-bottom: 1px solid #ccc;
	display: flex;
	align-items: center;
}
.pay-con-ctxt01{
	font-size: 30rpx;
	color: #0C101C;
	padding-right: 15rpx;
}
.pay-con-input{
	font-size: 30rpx;
	color: #9a9da3;
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

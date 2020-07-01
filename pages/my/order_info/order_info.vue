<template>
	<view>
		<view v-if="!isDuanWang">
			<!-- 1，待付款 2、已付款 3.已发货 4.已收货  -->
			<view :class="type==1||type==3?'orderInfo-tit01':'orderInfo-tit01 tit-bg'">
				<text class="orderInfo-tit-c01" v-if="type==3">待收货</text>
				<text class="orderInfo-tit-c01" v-if="type==1">待付款</text>
				<text class="orderInfo-tit-c02" v-if="type==2">已付款</text>
				<text class="orderInfo-tit-c02" v-if="type==4">待评价</text>
			</view>
			<view class="orderInfo-con01">
				<view class="orderInfo-con-c01 flex flex-sb mag-bottom3">
					<text class="info-ctxt01">收货地址</text>
					<text class="info-ctxt02">四川省遂宁市船山区幸福街道幸福街520号</text>
				</view>
				<view class="orderInfo-con-c01 flex flex-sb">
					<text class="info-ctxt01">收件人</text>
					<view class="flex">
						<text class="info-ctxt02">张明明</text>
						<text class="info-ctxt03">12311111111</text>
					</view>
				</view>
			</view>
			<view class="orderInfo-con01">
				<view class="orderInfo-con-tit">商品清单</view>
				<view class="orderInfo-con-list">
					<view class="orderInfo-list-c01">
						<view class="orderInfo-cli-txt01">商品名称商品名称商品名称商品名称商品名称商品名称商品名称商品名称商品名</view>
						<view class="flex">
							<text class="cli-ctxt01">数量:1</text>
							<text class="cli-ctxt01">单价:￥100</text>
						</view>
					</view>
					<view class="orderInfo-list-c01">
						<view class="orderInfo-cli-txt01">商品名称商品名称商品名称商品名称商品名称商品名称商品名称商品名称商品名</view>
						<view class="flex">
							<text class="cli-ctxt01">数量:1</text>
							<text class="cli-ctxt01">单价:￥100</text>
						</view>
					</view>
				</view>
			</view>
			<view class="orderInfo-con01">
				<view class="orderInfo-con-c01 flex flex-sb mag-bottom3">
					<text class="info-ctxt01">订单编号</text>
					<text class="info-ctxt02">000000000001</text>
				</view>
				<view class="orderInfo-con-c01 flex flex-sb mag-bottom3">
					<text class="info-ctxt01">数量</text>
					<text class="info-ctxt02">2</text>
				</view>
				<view class="orderInfo-con-c01 flex flex-sb mag-bottom3">
					<text class="info-ctxt01">商品实付</text>
					<text class="info-ctxt02">￥40</text>
				</view>
				<view class="orderInfo-con-c01 flex flex-sb mag-bottom3">
					<text class="info-ctxt01">支付方式</text>
					<text class="info-ctxt02">微信支付</text>
				</view>
				<view class="orderInfo-con-c01 flex flex-sb">
					<text class="info-ctxt01">时间</text>
					<text class="info-ctxt02">2019-10-12 10: 14: 17</text>
				</view>
			</view>
			<!-- 1，待付款 2、已付款 3.已发货 4.已收货 -->
			<view class="orderInfo-btn" v-if="type==1||type==3||type==4">
				<button v-if="type==3" class="info-btn01" hover-class="none">确认收货</button>
				<button v-if="type==1" class="info-btn02" hover-class="none" @click="cancelBtn">取消订单</button>
				<button v-if="type==1" class="info-btn01" hover-class="none" @click="payBtn">去付款</button>
				<button v-if="type==4" class="info-btn01" hover-class="none" @click="goPj">去评价</button>
			</view>
		</view>
		<!-- 取消订单弹窗 start-->
		<view class="popup" v-show="isCancel" @touchmove.stop.prevent="moveHandle">
			<view class="order-popup animated fadeIn">
				<view class='order-cancel-tit'>提示</view>
				<view class="order-cancel-txt">
					您确定要取消该订单吗？
				</view>
				<view class="order-cancel-btn">
					<button class="cancel-pop-btn01" @click="cancelBtn">取消</button>
					<button class="cancel-pop-btn02">确认</button>
				</view>
			</view>
		</view>
		<!-- 取消订单弹窗 end>-->
		<view class="popup" v-show="isPay" @touchmove.stop.prevent="moveHandle">
			<view class="faBack" @click="faHideClick()"></view>
			<view class="popup-pay animated fadeIn">
				<view class="pay-popup-con">
					<view class="pay-pop-con01">在线支付</view>
					<view class="pay-pop-ctxt01">选择支付方式</view>
					<view class="pay-pop-con02" v-for="(item,index) in payList" :key='index' @click="selPay(index)">
						<view class="pay-con-way01">
							<image :src="item.img"></image>
							<text>{{item.name}}</text>
						</view>
						<view class="pay-con-rad">
							<image :src="payType==index? '../../../static/image/Single_a.png':'../../../static/image/Single_aa.png'"></image>
						</view>
					</view>
					<view class="pay-pop-con03">
						<button class="pay-btn">确认</button>
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
				/* 1，待付款 2、已付款 3.已发货 4.已收货 */
				type:4,
				/* 取消订单 */
				isCancel:false,
				/* 去付款 */
				isPay:false,
				payType:1,
				payList:[
					{
						img:'../../../static/image/payment_a.png',
						name:'支付宝支付'
					},
					{
						img:'../../../static/image/payment_b.png',
						name:'微信支付'
					},
					{
						img:'../../../static/image/payment_c.png',
						name:'余额支付'
					}
				]
			}
		},
		methods: {
			/* 去评价 */
			goPj(){
				uni.navigateTo({
					url:'/pages/my/order_pj/order_pj'
				})
			},
			/* 取消订单弹窗 */
			cancelBtn(){
				this.isCancel = !this.isCancel
			},
			/* 取消订单弹窗 */
			payBtn(){
				this.isPay = !this.isPay
			},
			/* 点击蒙层关闭弹窗 */
			faHideClick(){
				this.isPay = false
			},
			/* 选择支付方式 */
			selPay(index){
				this.payType = index
			}
		}
	}
</script>

<style>
page{
	background: #F7F7F7;
}
.orderInfo-tit01{
	width: 100%;
	height: 60rpx;
	background: #f5e2e2;
}
.tit-bg{
	background: #def0e8;
}
.orderInfo-tit-c01{
	padding-left: 30rpx;
	font-size: 26rpx;
	color: #E5252A;
}
.orderInfo-tit-c02{
	padding-left: 30rpx;
	font-size: 26rpx;
	color: #03b463;
}
.orderInfo-con01{
	margin-bottom: 30rpx;
	padding: 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	background: #fff;
}
.orderInfo-con-c01{
	width: 100%;
	align-items: center;
}
.info-ctxt01{
	font-size: 26rpx;
	color: #9A9DA3;
}
.info-ctxt02{
	font-size: 26rpx;
	color: #0C101C;
}
.info-ctxt03{
	margin-left: 20rpx;
	padding-left: 20rpx;
	font-size: 26rpx;
	color: #0C101C;
	position: relative;
}
.info-ctxt03::after{
	position: absolute;
	width: 2rpx;
	height: 34rpx;
	background: #eee;
	content: '';
	left: 0;
	top:0; 
	margin-top: -2rpx;
}
.orderInfo-con-tit{
	font-size: 28rpx;
	color: #0C101C;
	font-weight: bold;
}
.orderInfo-con-list{
	width: 100%;
	height: auto;
}
.orderInfo-list-c01{
	width: 100%;
	height: auto;
	border-bottom: 1px solid #eee;
	padding-bottom: 30rpx;
}
.orderInfo-list-c01:last-child{
	border-bottom: 0px;
	padding-bottom: 0;
}
.orderInfo-cli-txt01{
	padding: 30rpx 0;
	width: 100%;
	font-size: 28rpx;
	color: #0C101C;
}
.cli-ctxt01{
	margin-right: 30rpx;
	font-size: 24rpx;
	color: #9A9DA3;
}
.orderInfo-btn{
	padding-right: 30rpx;
	width: calc( 100% - 30rpx );
	height: 100rpx;
	background: #fff;
	position: fixed;
	bottom: 0;
	left: 0;
	box-shadow: 0 0 15px #ccc;
	display: flex;
	justify-content: flex-end;
	align-items: center;
}
.orderInfo-btn button{
	width: 175rpx;
	height: 60rpx;
	line-height: 60rpx;
	background: #fff !important;
	font-size: 28rpx;
	border-radius: 40rpx;
	text-align: center;
	margin-left: 30rpx;
}
.info-btn01{
	border: 1rpx solid #E5252A;
	color: #E5252A;
}
.info-btn02{
	border: 1rpx solid #cecece;
	color: #0C101C;
}
</style>

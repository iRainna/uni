<template>
	<view>
		<view v-if="!isDuanWang">
			<!-- 头部 -->
			<view class="set-head">
				<view class="set-head-img01" @click="goBack"><image src="../../../static/image/nav_Return.png"></image></view>
				<view class="set-head-txt01">我的订单</view>
				<view class="set-head-txt02">保存</view>
			</view>
			<view class="set-name">
				<input placeholder="千小喵" />
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
			/* 返回上一级 */
			goBack(){
				uni.navigateBack({
					delta:1
				})
			}
		}
	}
</script>

<style>
page{
	background: #F7F7F7;
}
.set-head{
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
.set-head-img01{
	margin-left: 30rpx;
	width: 44rpx;
	height: 44rpx;
}
.set-head-img01 > image{
	width: 100%;
	height: 100%;
	display: block;
}
.set-head-txt01{
	flex: 1;
	text-align: center;
	font-size: 32rpx;
	color: #000000;
}
.set-head-txt02{
	margin-right: 30rpx;
	font-size: 28rpx;
	color: #03b463;
}
.set-name{
	margin-top: 180rpx;
	padding: 0 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
}
.set-name input{
	padding: 30rpx 0;
	width: 100%;
	border-bottom: 1px solid #dbd8d8;
}
</style>

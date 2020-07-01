<template>
	<view class="duan"  v-show="duanWang">
		<image src="../../static/wua.png" mode=""></image>
		<text>网络出错了~</text>
		<button hover-class="none"  @tap="changeType">重新连接</button>
	</view>
</template>

<script>
export default {
	name: 'duan',
	props: {
		duanWang: {
			type: Boolean,
			default: true
		},
	},
	data() {
		return {};
	},
	methods: {
		changeType:function(type){
		    this.$emit("reload")
		},
	}
};
</script>

<style>
.duan button {
	font-size: 26rpx;
	color: #fff !important;
	border-radius:10rpx;
	line-height: 66rpx;
	text-align: center;
	height: 66rpx;
	width: 180rpx;
	margin: 60rpx auto 0px auto;
	background-color: #cf9b0e !important;
}

.duan image {
	display: block;
	width: 310rpx;
	height: 200rpx;
}

.duan text{
	font-size: 26rpx;
	color: #999;
	display: block;
	text-align: center;
}

.duan {
	overflow: hidden;
	width: 310rpx;
	height: auto;
	margin: 40% auto 0px auto;
}
</style>

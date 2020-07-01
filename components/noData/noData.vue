<template>
	<view class="noData" v-show="nodata">
		<image src="../../static/no.png" mode=""></image>
		<text>{{ isNoText }}</text>
		<button type="default" v-show="isBtnShow" @tap="noTiao">{{ isNoBtnText }}</button>
	</view>
</template>

<script>
export default {
	name: 'noData',
	props: {
		nodata:{
			type: Boolean,
			default: false
		},
		isNoText: {
			type: String,
			default: ''
		},
		isBtnShow:{
			type: Boolean,
			default: false
		},
		isNoBtnText: {
			type: String,
			default: ''
		},
	},
	data() {
		return {
			noBtn:''
		};
	},
	methods: {
		noTiao(e) {
		this.$emit("click","index")
		},
	}
};
</script>

<style>
	.noData button {
		font-size: 26rpx;
		color: #fff !important;
		border-radius:10rpx;
		line-height: 66rpx;
		text-align: center;
		height: 66rpx;
		width: 180rpx;
		margin:40rpx auto 0px auto;
		background-color: #cf9b0e !important;
	}
	
	.noData text{
		font-size: 28rpx;
		color: #666;
		display: block;
		text-align: center;
	}
	
	.noData image{
		display: block;
		width: 270rpx;
		height: 187rpx;
		margin: 0 auto;
	}
	
	.noData{
		overflow: hidden;
		margin-top: 30%;
	}
</style>

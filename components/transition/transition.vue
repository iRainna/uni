<template>
	<view class="transition_div">
		<!-- 页面全屏过渡 -->
		<view class="transition " v-show="transition"><image src="../../static/loadGif.gif" mode=""></image></view>
		<!-- 小图标-->
		<view class="loading" v-show="loading">
			<image src="../../static/loadGif.gif" mode=""></image>
		</view>
	</view>
</template>

<script>
export default {
	name: 'transition',
	props: {
		transition: {
			type: Boolean,
			default: false
		},
		loading: {
			type: Boolean,
			default: false
		},
	},
	data() {
		return {};
	},
	methods: {}
};
</script>

<style>

.loading image{
	display: block;
	width: 100%;
	height: 100%;
}	

.loading{
	overflow: hidden;
	width: 200rpx;
	height: 200rpx;
	margin: 36% auto 0px auto;
	    margin: -19% auto 0px auto;
	    position: fixed;
	    left: 50%;
	    top: 50%;
	    margin-left: -100rpx;
	    z-index: 200;
}
	
.transition_div {
	overflow: hidden;
}

.guo {
	overflow: hidden;
	width: 100%;
	height: 100%;
	background-color: red;
	position: fixed;
	left: 0;
	top: 0;
	z-index: 200;
}

.transition {
	overflow: hidden;
	width: 100%;
	height: 100%;
	position: fixed;
	left: 0px;
	top: 0;
	z-index: 200;
	display: flex;
	background-color: #fff;
}

.transition image {
	display: block;
	width: 200rpx;
	height: 200rpx;
	margin: 0 auto;
	position: absolute;
	left: 50%;
	top: 36%;
	margin-left: -100rpx;
	margin-top: -100rpx;
	z-index: 210;
}
</style>

<template>
	<view class="moreText uni-loadmore  center zhong" v-if="showLoadMore">
		<image src="../../static/loading_more.gif" v-show="isNoLoad"></image>
		<text>{{ loadMoreText }}</text>
	</view>
</template>

<script>
	export default {
		name: "moreText",
		props:{
			showLoadMore:{
				type: Boolean,
				default: true
			},
			loadMoreText:{
				type:String,
				default:''
			},
			isNoLoad:{
				type: Boolean,
				default: true
			},
		},
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>
<style>
	.moreText>image {
		display: block;
		width: 22rpx;
		height: 22rpx;
		margin-right: 1em;
	}
	
	.moreText {
		overflow: hidden;
		display: flex;
		margin: 30rpx auto;
	}
	
	.moreText text {
		overflow: hidden;
		font-size: 26rpx;
		color: #666;
	}
</style>

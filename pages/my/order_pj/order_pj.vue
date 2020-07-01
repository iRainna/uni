<template>
	<view>
		<view v-if="!isDuanWang">
			<view class="orderPj-con01">
				<textarea placeholder="请输入您的评价~"></textarea>
			</view>
			<view class="orderPj-star">
				<image v-for="(star,index) in stars" :key='index' :src="star.src"></image>
			</view>
			<view class="orderPj-btn">
				<button class="pj-btn01" hover-class="none">提交</button>
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
				/* 评分 */
				stars: [
				    {src: "../../../static/image/star_a.png"},
				    {src: "../../../static/image/star_aa.png"},
					{src: "../../../static/image/star_aa.png"},
				    {src: "../../../static/image/star_aa.png"},
				    {src: "../../../static/image/star_aa.png"},
				],
			}
		},
		methods: {
		}
	}
</script>

<style>
page{
	background: #F7F7F7;
}
.orderPj-con01{
	padding: 30rpx;
	margin: 30rpx auto;
	width: calc( 100% - 60rpx );
	height: auto;
	overflow: hidden;
	background: #fff;
}
.orderPj-con01 textarea{
	font-size: 28rpx;
	color: #0C101C;
}
.orderPj-star{
	padding: 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	overflow: hidden;
	background: #fff;
	display: flex;
	align-items: center;
}
.orderPj-star image{
	margin-right: 20rpx;
	width: 52rpx;
	height: 50rpx;
	display: block;
}
.orderPj-btn{
	padding:20rpx 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	background: #fff;
	position: fixed;
	bottom: 0;
	left: 0;
	box-shadow: 0 0 15px #ccc;
}
.pj-btn01{
	width: 100%;
	height: 90rpx;
	line-height: 90rpx;
	text-align: center;
	font-size: 28rpx;
	color: #fff;
	background-image: linear-gradient(to right, #e83035 , #fa7276) !important;
	border-radius: 10rpx;
}
</style>

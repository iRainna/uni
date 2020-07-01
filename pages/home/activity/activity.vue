<template>
	<view class="activity">
		
		<view class="ac_content">
			<text class="ac_title">{{activity.title}}</text>
			<br/>
			<text class="ac_time">{{activity.time}}</text>
			<br/>
			<text class="ac_content_text">{{activity.contentText}}</text>
			<br/>
			<image src="../../../static/image/picture_a.png" class="ac_bg" mode=""></image>
			<br/>
			<text class="ac_content_text2">{{activity.contentText}}</text>
			<br/>
			<button type="default" class="ac_btn" hover-class="none">查看课程详情</button>
		</view>
		
		
		
		<!-- 上拉加载更多图标和文字-->
		<load-more :showLoadMore="isMore" :isNoLoad="isNoLoad" :loadMoreText="loadMoreText"></load-more>
		<!-- 暂无数据 -->
		<no-data :isNoText="isNoText" :nodata="isNodata"></no-data>
		<!-- 断网 -->
		<duan-wang :duanWang="isDuanWang" v-on:reload="Refresh"></duan-wang>
		<!--过渡 -->
		<tran-sition :transition="isTransit" :loading="isLoading"></tran-sition>
	</view>
</template>

<script>
	// import Skeleton from '@/components/J-skeleton/J-skeleton.vue';
	import tranSition from '@/components/transition/transition.vue';
	import duanWang from '@/components/duanWang/duanWang.vue';
	import loadMore from '@/components/more/more.vue';
	import noData from '@/components/noData/noData.vue';
	export default {
		components: {
			// Skeleton,
			tranSition,
			duanWang,
			loadMore,
			noData
		},
		data() {
			return {
				isLiheight: false,
				isDuanWang: false, // 断网的图片：
				isNodata: false, //是否显示暂无数据
				isNoText: '暂无数据~',
				isTransit: false, //是否显示全屏过渡页面
				isLoading: false, //是否显示logo加载小图标
				isMore: true,
				loadMoreText: '',
				isNoLoad: false, //是否显示加载login
				// 轮播
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500,
				activity:{
					title:'活动标题活动标题',
					time:'2020-03-14',
					contentText:'　　天津理工大学经济与管理学院教授，主讲一级造价工程师《建设工程计价》。参与完成若干项国家、省部级研究课题，主持编写了全国造价工程师执业资格考试培训教材，同时主编、参编各种教材和专著7本;授课条理清晰、重点突出针对性强，重点、难点解析到位，能够带动学员思维，深受学员喜爱。'
				}
			}
			},
	}
</script>

<style>
	.ac_content{
		/* padding: 20rpx; */
		padding: 20rpx;
		
	}
	.ac_title{
		font-size: 40rpx;
		font-weight: bold;
	}
	.ac_time{
		font-size: 24rpx;color: rgb(154,158,162);
		background-color: rgb(243,243,247);
		padding-left: 14rpx;
		padding-right: 14rpx;
		padding-top:7rpx ;
		padding-bottom: 7rpx;
		border-radius: 5rpx;
		margin-top: 10px;
		    position: relative;
			top: 20rpx;
	}
	.ac_content_text{
		position: relative;
		    top: 40rpx;
			font-size: 28rpx;
	}
	.ac_bg{
		width: 690rpx;
		height: 222rpx;
		/* margin: 0 auto;
		display: inline-flex; */
		/* width: 331px;
		    height: 106px; */
		    /* margin: 0 auto; */
		    position: relative;
		    left: 50%;
		    top: 60rpx;
		    margin-left: -345rpx;
	}
	.ac_content_text2{
		position: relative;
		    top: 80rpx;
			font-size: 28rpx;
	}
	.ac_btn{
		position: relative;
		    top: 120rpx;
			width: 275rpx;
			height: 88rpx;
			border: solid 2rpx rgb(231,36,40);
			font-size: 30rpx;
			color:rgb(231,36,40) ;
			left: 50%;
			margin-left: -134rpx;
			background-color: white !important;
	}
</style>

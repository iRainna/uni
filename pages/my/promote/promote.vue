<template>
	<view>
		<view v-if="!isDuanWang">
			<view class="helpInfo-content">
				<view class="helpInfo-con">
					我公司主讲-级造价工程师《建设工程计价》。参与完成若干项国家、省部级研究课题，
					主持编写了全国造价工程师执业资格考试培训教材,同时主编、参编各种教材和专著7本;授课条理清晰、重点突出针对性强
					我公司主讲-级造价工程师《建设工程计价》。参与完成若干项国家、省部级研究课题
				</view>
				<view class="helpInfo-img"><image src="../../../static/image/picture_b.png"></image></view>
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
				isDuanWang: false
			}
		},
		methods: {
			
		}
	}
</script>

<style>
.helpInfo-content{
	padding: 40rpx 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	overflow: hidden;
	border-top: 1rpx solid #eee;
}
.helpInfo-con{
	width: 100%;
	height: auto;
	font-size: 26rpx;
	color: #0C101C;
	line-height: 50rpx;
	text-indent: 2em;
}
.helpInfo-img{
	margin: 30rpx auto;
	width: 100%;
	height: 220rpx;
}
.helpInfo-img image{
	width: 100%;
	height: 100%;
	display: block;
}
</style>


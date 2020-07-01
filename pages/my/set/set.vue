<template>
	<view>
		<view v-if="!isDuanWang" class="set">
			<view class="set-con">
				<view class="set-con02">
					<text>头像</text>
					<view class="set-con-img">
						<view class="set-img01">
							<image src="../../../static/image/head2.png"></image>
						</view>
						<image src="../../../static/image/choose.png" class="set-img02"></image>
					</view>
				</view>
				<view class="set-con01 flex flex-sb">
					<text>用户名</text>
					<view class="set-amend-btn" @click="goSetName">
						<text class="set-txt01">千小喵</text>
						<image src="../../../static/image/choose.png" class="set-img02"></image>
					</view>
				</view>
				<view class="set-con01 flex flex-sb">
					<text>电话号码</text>
					<view class="set-amend-btn">
						<text class="set-txt02">12544444444</text>
						<image src="../../../static/image/choose.png" class="set-img02"></image>
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
				//断网
				isDuanWang:false,
				userInfo:{},
				currInfo:{
					headImg:'',
					headImgId:'',
					userName:'',
					userRealyName:'',
					phone:'',
				},
				isClick:false,
				
			}
		},
		onLoad() {
		},
		methods: {
			goSetName(){
				uni.navigateTo({
					url:'/pages/my/set_name/set_name'
				})
			}
		},
		
		
		
	}
</script>

<style>
page{
	background: #f7f7f7;
}
.set{
	width: 100%;
	height: auto;
	border-top: 1px solid #E6E6E6;
}
.set-con{
	padding: 0 30rpx;
	width: calc(100%-60rpx);
	height: auto;
	background: #FFFFFF;
}
.set-con01{
	width: 100%;
	height: auto;
	padding: 30rpx 0;
	display: flex;
	align-items: center;
	border-bottom: 1px solid #E6E6E6;
}
.set-con01 >text{
	font-size: 28rpx;
	color: #333333;
	width: 120rpx;
	padding-right: 60rpx;
}
.set-con01 >input{
	color: #999;
	font-size: 28rpx;
	flex: 1;
}
.set-con01 .set-color{
	color: #333333;
	font-size: 28rpx;
	flex: 1;
}

.set-con02{
	width: 100%;
	height: auto;
	padding: 30rpx 0;
	display: flex;
	align-items: center;
	justify-content: space-between;
	border-bottom: 1px solid #E6E6E6;
}
.set-con02 >text{
	font-size: 28rpx;
	color: #333333;
	width: 120rpx;
	padding-right: 60rpx;
}
.set-con-img{
	display: flex;
	align-items: center;
}
.set-img01{
	width: 90rpx;
	height: 90rpx;
	background: url(../../../static/image/my_head.png);
	background-size: 100%;
	box-sizing: 100%;
	border-radius: 50%;
}
.set-img01 > image{
	width: 100%;
	height: 100%;
	display: block;
	border-radius: 50%;
}
.set-img02{
	margin-left: 15rpx;
	width: 11rpx;
	height: 24rpx;
	display: block;
}
.set-amend-btn{
	display: flex;
	align-items: center;
}
.set-txt02{
	background: #FFFFFF !important;
	font-size: 28rpx;
	color: #9A9DA3;
}
.set-txt01{
	color: #0C101C;
	font-size: 28rpx;
}
</style>

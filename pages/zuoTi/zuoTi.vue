<template>
	<view>
		<view v-if="!isDuanWang">
			<!-- 头部 -->
			<view class="zuoTi-head flex">
				<view class="zuoTi-head-img01" @click="goBack"><image src="../../static/image/nav_Return.png"></image></view>
				<view class="zuoTi-head-txt01">章节练习</view>
				<view class="zuoTi-head-btn">
					<button hover-class="none" @click="goTika">题卡</button>
				</view>
			</view>
			<view class="zuoTi-content">
				<view class="zuoTi-con">
					<view class="zuoTi-con-c01">
						<view class="flex flex-sb mag-bottom1">
							<view class="flex">
								<text class="zuoti-con-ctxt01">项目:</text>
								<text class="zuoti-con-ctxt02">教师资格证</text>
							</view>
							<view class="flex">
								<text class="zuoti-con-ctxt01">科目:</text>
								<text class="zuoti-con-ctxt02">语文</text>
							</view>
						</view>
						<view class="flex flex-sb mag-bottom1">
							<view class="flex">
								<text class="zuoti-con-ctxt01">总题数:</text>
								<text class="zuoti-con-ctxt02">10题</text>
							</view>
							<view class="flex">
								<text class="zuoti-con-ctxt01">未做:</text>
								<text class="zuoti-con-ctxt02">10题</text>
							</view>
						</view>
						<view class="flex flex-sb">
							<view class="flex">
								<text class="zuoti-con-ctxt01">单元:</text>
								<text class="zuoti-con-ctxt02">语文冲刺课第一单元</text>
							</view>
							
						</view>
					</view>
				</view>
				<!-- 做题 -->
				<view class="zuoti-con02">
					<view class="zuoti-title flex mag-bottom3">
						<text class="zuoti-c01 flex">
							<text class="zuoti-tit-t01">1</text>
							<text class="zuoti-tit-t02">/40</text>
							<text class="zuoti-txt01">【单选题】</text>
							<text class="zuoti-name">
								题目题目题目题目题目题目题目题目题目题目题目题目题目题目
							</text>
							<text class="zuoti-txt02">[1分]</text>
						</text>
					</view>
					<view class="zuoti-cli01 flex" @click="selRind(1)">
						<text :class="rad==1?'zuoti-rad rad-nav':'zuoti-rad'">A</text>
						<text class="zuoti-cli-txt">选项一</text>
					</view>
					<view class="zuoti-cli01 flex" @click="selRind(2)">
						<text :class="rad==2?'zuoti-rad rad-nav':'zuoti-rad'">B</text>
						<text class="zuoti-cli-txt">选项一</text>
					</view>
					<view class="zuoti-cli01 flex" @click="selRind(3)">
						<text :class="rad==3?'zuoti-rad rad-nav':'zuoti-rad'">C</text>
						<text class="zuoti-cli-txt">选项一</text>
					</view>
					<view class="zuoti-cli01 flex" @click="selRind(4)">
						<text :class="rad==4?'zuoti-rad rad-nav':'zuoti-rad'">D</text>
						<text class="zuoti-cli-txt">选项一</text>
					</view>
				</view>
			</view>
			<view class="zuoti-con-btn">
				<view class="zuoti-btn01">
					<image src="../../static/image/examination_b.png"></image>
					<text>检查</text>
				</view>
				<view class="zuoti-btn01">
					<image src="../../static/image/examination_a.png"></image>
					<text>保存</text>
				</view>
				<view class="zuoti-btn01">
					<image src="../../static/image/examination_c.png"></image>
					<text>交卷</text>
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
				rad:1
			}
		},
		methods: {
			/* 返回上级 */
			goBack(){
				uni.navigateBack({
					delta:1
				})
			},
			/* 选择题目 */
			selRind(id){
				this.rad = id
			},
			/* 题卡 */
			goTika(){
				uni.navigateTo({
					url:'/pages/tika/tika'
				})
			}
		}
	}
</script>

<style>
page{
	background: #F7F7F7;
}
.zuoTi-head{
	padding-top: 44rpx;
	width: 100%;
	height: 88rpx;
	background: #fff;
	display: flex;
	justify-content: space-between;
	align-items: center;
	position: fixed;
	top: 0;
	left: 0;
	z-index: 13;
}
.zuoTi-head-img01{
	margin-left: 30rpx;
	width: 44rpx;
	height: 44rpx;
}
.zuoTi-head-img01 > image{
	width: 100%;
	height: 100%;
	display: block;
}
.zuoTi-head-txt01{
	flex: 1;
	text-align: center;
	font-size: 32rpx;
	color: #000000;
}
.zuoTi-head-btn{
	margin-right: 30rpx;
}
.zuoTi-head-btn button{
	width: 120rpx;
	height: 50rpx;
	line-height: 50rpx;
	border: 1px solid #0c101c;
	border-radius: 8rpx;
	text-align: center;
	font-size: 28rpx;
	color: #0C101C;
	background: #fff!important;
}
.zuoTi-content{
	padding-bottom: 30rpx;
	margin-top: 160rpx;
	width: 100%;
	height: auto;
	overflow: hidden;
	background: #fff;
}
.zuoTi-con{
	padding:30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	overflow: hidden;
	background: #fff;
}
.zuoTi-con-c01{
	padding: 30rpx;
	height: auto;
	width: calc( 100% - 60rpx );
	background: #f6f8fc;
}
.zuoti-con-ctxt01{
	padding-right: 15rpx;
	font-size: 26rpx;
	color: #9A9DA3;
}
.zuoti-con-ctxt02{
	font-size: 26rpx;
	color: #0C101C;
}
.zuoti-con02{
	padding: 0 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	overflow: hidden;
}
.zuoti-title{
	width: 100%;
	align-items: center;
}

.zuoti-tit-t01{
	font-size: 28rpx;
	color: #E5252A;
}
.zuoti-tit-t02{
	font-size: 28rpx;
	color: #9A9DA3;
}
.zuoti-txt01{
	font-size: 30rpx;
	color: #E5252A;
}
.zuoti-name{
	font-size: 30rpx;
	color: #0C101C;
}
.zuoti-txt02{
	padding-left: 15rpx;
	font-size: 26rpx;
	color: #9A9DA3;
}
.zuoti-cli01{
	margin-bottom: 20rpx;
	padding: 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	border: 1px solid #eee;
	align-items: center;
}
.zuoti-rad{
	width: 40rpx;
	height: 40rpx;
	text-align: center;
	line-height: 40rpx;
	border: 1px solid #b6b9bd;
	border-radius: 50%;
	font-size: 24rpx;
	color: #9A9DA3;
	margin-right: 30rpx;
}
.rad-nav{
	background: #fbe3ec;
	color: #ec74a1;
	border: 1px solid #fbe3ec;
}
.zuoti-cli-txt{
	font-size: 30rpx;
	color: #0C101C;
}
.zuoti-con-btn{
	padding: 15rpx 0;
	width: 100%;
	height: auto;
	background: #fff;
	border-top: 1px solid #CECECE;
	display: flex;
	position: fixed;
	bottom: 0;
	left: 0;
}
.zuoti-btn01{
	width: calc( 100% / 3 );
	height: auto;
}
.zuoti-btn01 image{
	width: 44rpx;
	height: 44rpx;
	margin: 0 auto;
	display: block;
}
.zuoti-btn01 text{
	width: 100%;
	text-align: center;
	font-size: 28rpx;
	color: #9A9DA3;
	display: block;
}
</style>

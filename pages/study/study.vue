<template>
	<view>
		<view v-if="!isDuanWang">
			<!-- 头部 -->
			<view class="study-head flex">
				<view class="study-head-tit">
					<text :class="tit==1?'head-link':''" @click="selTit(1)">全部</text>
					<text :class="tit==2?'head-link':''" @click="selTit(2)">免费课</text>
					<text :class="tit==3?'head-link':''" @click="selTit(3)">付费课</text>
				</view>
				<view class="study-head-img" @click="menu">
					<image src="../../static/image/spot01.png"></image>
				</view>
				<view class="study-head-nav" v-show="isMenu">
					<view class="study-nav-c01">我的错题</view>
					<view class="study-nav-c01">习题记录</view>
					<view class="study-nav-c01">我的笔记</view>
				</view>
			</view>
			<!-- 内容 -->
			<view class="study-content">
				<view class="study-con01" v-for="(item,index) in list" :key='index' @click="goList">
					<view class="study-con-name mag-bottom3">{{item.name}}</view>
					<view class="study-con-cli01 flex mag-bottom3">
						<text class="study-con-ctxt01">{{item.tab}}</text>
						<text class="study-con-ctxt02">课程距离到期时间还剩</text>
						<text class="study-con-ctxt03">{{item.time}}</text>
						<text class="study-con-ctxt02">天</text>
					</view>
					<view class="study-con-cli01 flex mag-bottom3">
						<text class="con-cli-ctx01">学习进度</text>
						<view class="study-con-bar"><view class="study-con-cbar" :style="{width: item.study}"></view></view>
						<text class="con-cli-ctx02">{{item.study}}</text>
					</view>
					<view class="study-con-cli01 flex">
						<text class="con-cli-ctx01">模考进度</text>
						<view class="study-con-bar"><view class="study-con-cbar" :style="{width: item.exam}"></view></view>
						<text class="con-cli-ctx02">{{item.exam}}</text>
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
				/* 头部导航 */
				isMenu:false,
				// 断网：
				isDuanWang: false,
				tit:1,
				list:[
					{
						name:'课程名称课程名称课程名称课程名称课程名称',
						tab:'一级建造师',
						time:'99',
						study:'30%',
						exam:'30%'
					},{
						name:'课程名称课程名称课程名称课程名称课程名称',
						tab:'一级建造师',
						time:'99',
						study:'50%',
						exam:'30%'
					},{
						name:'课程名称课程名称课程名称课程名称课程名称',
						tab:'一级建造师',
						time:'99',
						study:'50%',
						exam:'20%'
					},{
						name:'课程名称课程名称课程名称课程名称课程名称',
						tab:'一级建造师',
						time:'99',
						study:'80%',
						exam:'70%'
					}
				]
			}
		},
		methods: {
			/* 切换 */
			selTit(id){
				this.tit = id
			},
			/* 头部导航 */
			menu(){
				this.isMenu = !this.isMenu
			},
			/* 科目列表0 */
			goList(){
				uni.navigateTo({
					url:'/pages/study_list/study_list'
				})
			}
		}
	}
</script>

<style>
page{
	background: #F7F7F7;
}
.study-head-nav{
	padding: 0 30rpx;
	position: fixed;
	right: 0;
	width: 160rpx;
	height: 270rpx;
	background: #4c4c4c;
	border-radius: 10rpx;
	top:150rpx
}
.study-head-nav::before{
	content:" ";
	width: 0;  
    height: 0;  
    overflow: hidden;
    font-size: 0;
    line-height: 0;            
    border-width: 20rpx;               
    border-style: solid;
    border-color: transparent transparent #4c4c4c transparent;
	position: absolute;
	right:15px;
	top:-38rpx;
}
.study-nav-c01{
	padding: 30rpx 0;
	width: 100%;
	font-size: 24rpx;
	color: #fff;
	text-align: center;
	border-bottom: 1rpx solid #666;
}
.study-nav-c01:last-child{
	border-bottom: 0px;
}
.study-head{
	width: 100%;
	height: 88rpx;
	padding-top: 44rpx;
	align-items: center;
	justify-content: flex-end;
	background: #FFFFFF;
	position: fixed;
	top: 0;
	left: 0;
	z-index: 13;
}
.study-head-tit{
	width: calc( 100% - 74rpx );
	display: flex;
}
.study-head-tit text{
	width: calc( ( 100% - 74rpx ) / 3 );
	font-size: 30rpx;
	color: #9A9DA3;
	text-align: center;
	position: relative;
}
.study-head-tit text::after{
	position: absolute;
	content: '';
	width: 30rpx;
	height: 5rpx;
	background: #fff;
	bottom: 0;
	left: 50%;
	margin-left: -15rpx;
	margin-bottom: -10rpx;
}
.study-head-tit .head-link::after{
	background: #0C101C;
}
.study-head-tit .head-link{
	color: #0C101C;
	font-weight: bold;
}
.study-head-img{
	width: 44rpx;
	height: 44rpx;
	margin-right: 30rpx;
}
.study-head-img image{
	width: 100%;
	height: 100%;
	display: block;
}
.study-content{
	margin-top: 140rpx;
	padding: 30rpx 0;
	width: 100%;
	height: auto;
	overflow: hidden;
}
.study-con01{
	margin-bottom: 30rpx;
	padding:30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	overflow: hidden;
	background: #fff;
}
.study-con-name{
	width: 100%;
	font-size: 30rpx;
	color: #0C101C;
}
.study-con-cli01{
	width: 100%;
	overflow: hidden;
	align-items: center;
}
.study-con-ctxt01{
	margin-right: 20rpx;
	font-size: 24rpx;
	color: #9A9DA3;
	background: #f5f7fb;
	padding: 10rpx 20rpx;
	border-radius: 8rpx;
}
.study-con-ctxt02{
	font-size: 24rpx;
	color: #9A9DA3;
}
.study-con-ctxt03{
	padding: 0 10rpx;
	font-size: 24rpx;
	color: #E83035;
}
.con-cli-ctx01{
	font-size: 28rpx;
	color: #9A9DA3;
}
.con-cli-ctx02{
	font-size: 26rpx;
	color: #E5252A;
}
.study-con-bar{
	width: 430rpx;
	margin: 0 25rpx;
	height: 13rpx;
	background: #f7f7f7;
	position: relative;
	border-radius: 30rpx;
}
.study-con-cbar{
	position: absolute;
	width: 50%;
	height: 100%;
	background: linear-gradient(to right,#fca3a4,#e8373c);
	top:0;
	left: 0;
	border-radius: 30rpx;
}
</style>

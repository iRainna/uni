<template>
	<view>
		<view v-if="!isDuanWang">
			<!-- 头部 -->
			<view class="test-head">
				<view class="test-head-tit flex">
					<image src="../../static/image/search.png"></image>
					<input placeholder="搜索考试名称、老师名称或课程名称" />
				</view>
			</view>
			<!-- 内容 -->
			<view class="test-content">
				<view class="test-con-left">
					<view :class="link==index?'test-left-c01 test-left-link':'test-left-c01'" @click="tabNav(index)" 
					v-for="(item,index) in list" :key='index'>
						{{item.name}}
					</view>
				</view>
				<view class="test-con-right">
					<view class="test-right-c01" v-for="(item,index) in list1" :key='index'>
						<view class="test-right-ct01 flex">
							<text class="test-cri-txt01">{{item.con01}}-</text>
							<text class="test-cri-txt02">{{item.con02}}</text>
						</view>
						<view class="test-right-list">
							<view class="test-right-li" v-for="(t,id) in item.liName" :key='id'>
								<text>{{t.name}}</text>
							</view>
						</view>
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
				// 断网：
				isDuanWang: false,
				/* 左侧分类 */
				list:[
					{name:'建筑工程'},
					{name:'建筑工程'},
					{name:'新职业技能'},
					{name:'建筑工程'},
					{name:'建筑工程'},
					{name:'建筑工程'},
					{name:'建筑工程'},
					{name:'建筑工程'},
					{name:'建筑工程'},
					{name:'建筑工程'}
				],
				link:'',
				list1:[
					{
						con01:'建造工程',
						con02:'消防安全',
						liName:[
							{name:'二级建造工程'},
							{name:'二级建造师'},
							{name:'一级工程实训网'},
							{name:'一级工程实训网'},
							{name:'一级工程实训网'},
						]
					},{
						con01:'建造工程',
						con02:'消防安全',
						liName:[
							{name:'二级建造工程'},
							{name:'二级建造师'},
							{name:'一级工程实训网'},
							{name:'一级工程实训网'},
							{name:'一级工程实训网'},
						]
					},{
						con01:'建造工程',
						con02:'消防安全',
						liName:[
							{name:'二级建造工程'},
							{name:'二级建造师'},
							{name:'一级工程实训网'},
							{name:'一级工程实训网'},
							{name:'一级工程实训网'},
						]
					}
				]
			}
		},
		methods: {
			tabNav(index){
				this.link = index;
			}
		}
	}
</script>

<style>
.test-head{
	padding: 44rpx 30rpx 10rpx 30rpx;
	width: calc( 100% - 60rpx );
	height: 88rpx;
	line-height: 88rpx;
	position: fixed;
	top: 0;
	left: 0;
	background: #fff;
	z-index: 13;
}
.test-head-tit{
	width: 100%;
	height: 70rpx;
	background: #f7f7f7;
	border-radius: 40rpx;
	align-items: center;
}
.test-head-tit image{
	margin: 0 20rpx;
	width: 28rpx;
	height: 28rpx;
	display: block;
}
.test-head-tit input{
	font-size: 28rpx;
	color: #9A9DA3;
}
.test-content{
	border-top: 1px solid #eee;
	display: flex;
	width: 100%;
	height: auto;
	overflow: hidden;
	margin-top: 150rpx;
}
.test-con-left{
	width: 185rpx;
	height: auto;
	overflow: hidden;
	background: #f7f7f7;
}
.test-left-c01{
	width: 100%;
	height: 100rpx;
	font-size: 28rpx;
	color: #9A9DA3;
	text-align: center;
	line-height: 100rpx;
	position: relative;
}
.test-left-c01::after{
	position: absolute;
	width: 7rpx;
	height: 30rpx;
	background: #F7F7F7;
	content: '';
	left: 10rpx;
	top:50%;
	margin-top: -15rpx;
}
.test-left-link::after{
	background: #0C101C;
}
.test-left-link{
	color: #0C101C;
	font-weight: bold;
	background: #fff;
}

.test-con-right{
	padding: 0 30rpx 0 20rpx;
	width: calc( 100% - 235rpx );
	height: auto;
	overflow: hidden;
	background: #fff;
}
.test-right-c01{
	width: 100%;
	height: auto;
	overflow:hidden ;
}
.test-right-ct01{
	width: 100%;
	overflow: hidden;
	padding: 50rpx 0 30rpx 0;
}
.test-cri-txt01{
	font-size: 28rpx;
	color: #9A9DA3;
}
.test-cri-txt02{
	font-size: 30rpx;
	font-weight: bold;
	color: #0C101C;
}
.test-right-list{
	width: 100%;
	height: auto;
	overflow: hidden;
	display: flex;
	flex-wrap: wrap;
}
.test-right-li{
	width: 140rpx;
	background: #f5f7fb;
	border-radius: 10rpx;
	padding: 20rpx 10rpx;
	margin-bottom: 20rpx;
	margin-right: 15rpx;
}
.test-right-li:last-child{
	margin-right: 0rpx;
}
.test-right-li:nth-child(3n+3){
	margin-right: 0rpx;
}
.test-right-li text{
	font-size: 12px;
	color: #0C101C;
	display: block;
	padding-left: 10px;
	padding-right: 10px;
	text-align: center;
	display: -webkit-box;
	-webkit-box-orient: vertical;
	-webkit-line-clamp: 2;
	overflow: hidden;
}
</style>

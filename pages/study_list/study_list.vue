<template>
	<view>
		<view v-if="!isDuanWang">
			<view class="study-list-content mag-bottom3">
				<view class="study-list-con01">
					<view class="study-cli-ctit">课程名称课程名称课程名称课程名称课程名称课程名</view>
					<view class="study-cli-txt01">课程有效期截至于2020年3月30日</view>
					<view class="flex">
						<text class="cli-txt01">课程距离到期时间还剩</text>
						<text class="cli-txt02">150</text>
						<text class="cli-txt01">天</text>
					</view>
				</view>
				<view class="study-list-con02">
					<view class="study-cli-c01" @click="goTestPaper">
						<image src="../../static/image/subject_a.png"></image>
						<text>模拟考试</text>
					</view>
					<view class="study-cli-c01" @click="goTestPaper">
						<image src="../../static/image/subject_b.png"></image>
						<text>历年真题</text>
					</view>
					<view class="study-cli-c01" @click="goSection">
						<image src="../../static/image/subject_c.png"></image>
						<text>章节练习</text>
					</view>
					<view class="study-cli-c01" @click="goTestPaper">
						<image src="../../static/image/subject_d.png"></image>
						<text>考前押题</text>
					</view>
					<view class="study-cli-c01" @click="goZhishi">
						<image src="../../static/image/subject_e.png"></image>
						<text>高频考点</text>
					</view>
					<view class="study-cli-c01" @click="goZuoTi">
						<image src="../../static/image/subject_f.png"></image>
						<text>每日一练</text>
					</view>
					<view class="study-cli-c01" @click="goZhishi">
						<image src="../../static/image/subject_g.png"></image>
						<text>全部知识点</text>
					</view>
				</view>
			</view>
			<view class="study-list-content">
				<view class="study-cli02-tit">快速学习</view>
				<view class="study-cli02-list">
					<view class="list-con01" v-for="(item,index) in list" :key='index'>
						<view class="list-con01-tab">
							<text v-if="item.isZhibo==false">录</text>
							<text v-if="item.isZhibo==true">直播</text>
						</view>
						<view class="list-con01-cent01">{{item.con}}</view>
						<view class="list-con01-cent02 flex" v-if="item.isZhibo==false">
							<text>已更新{{item.finish1}}讲</text>
							<text>已完成{{item.finish2}}讲</text>
						</view>
						<view class="list-con01-cent02 flex flex-sb" v-if="item.isZhibo==true">
							<text>{{item.time}}</text>
							<button class="list-con-btn" hover-class="none">立即预约</button>
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
				list:[
					{
						con:'备考指导班(技能四级)',
						finish1:'4',
						finish2:'7',
						isZhibo:false,
						time:'2020-01-01 12:20~14:30'
					},
					{
						con:'备考指导班(技能四级)',
						finish1:'4',
						finish2:'7',
						isZhibo:true,
						time:'2020-01-01 12:20~14:30'
					},{
						con:'备考指导班(技能四级)',
						finish1:'4',
						finish2:'7',
						isZhibo:false,
						time:'2020-01-01 12:20~14:30'
					}
				]
			}
		},
		methods: {
			/* 模拟考试，历年真题，考前押题 */
			goTestPaper(){
				uni.navigateTo({
					url:'/pages/test_paper/test_paper'
				})
			},
			/* 章节练习 */
			goSection(){
				uni.navigateTo({
					url:'/pages/section/section'
				})
			},
			/* 知识点 */
			goZhishi(){
				uni.navigateTo({
					url:'/pages/zhishi/zhishi'
				})
			},
			/* 每日一练 */
			goZuoTi(){
				uni.navigateTo({
					url:'/pages/zuoTi/zuoTi'
				})
			}
		}
	}
</script>

<style>
page{
	background: #F7F7F7;
}
.study-list-content{
	width:100%;
	height: auto;
	overflow: hidden;
	background: #fff;
}
.study-list-con01{
	padding: 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	overflow: hidden;
	border-bottom: 1px solid #eee;
}
.study-cli-ctit{
	width: 100%;
	max-height: 90rpx;
	font-size: 28rpx;
	line-height: 44rpx;
	color: #0C101C;
	overflow: hidden;
	text-overflow: ellipsis;
	display: -webkit-box;
	-webkit-line-clamp: 2;
	-webkit-box-orient: vertical;
}
.study-cli-txt01{
	padding: 20rpx 0;
	font-size: 26rpx;
	color: #9A9DA3;
}
.cli-txt01{
	font-size: 26rpx;
	color: #9A9DA3;
}
.cli-txt02{
	font-size: 26rpx;
	color: #E5252A;
}
.study-list-con02{
	margin-top: 30rpx;
	width: 100%;
	height: auto;
	overflow: hidden;
	display: flex;
	flex-wrap: wrap;
	align-items: center;
}
.study-cli-c01{
	margin-bottom: 30rpx;
	width: calc( 100% / 4 );
	height: auto;
	overflow: hidden;
}
.study-cli-c01 image{
	margin: 0 auto;
	width: 88rpx;
	height: 88rpx;
	display: block;
}
.study-cli-c01 text{
	width: 100%;
	display: block;
	text-align: center;
	font-size: 28rpx;
	color: #0C101C;
}
/* study-cli02-tit */
.study-cli02-tit{
	padding: 30rpx;
	font-size: 28rpx;
	color: #0C101C;
	font-weight: bold;
}
.study-cli02-list{
	padding: 0 30rpx;
	height: auto;
	width: calc( 100% - 60rpx );
	overflow: hidden;
}
.list-con01{
	padding: 20rpx 0;
	width: 100%;
	height: auto;
	overflow: hidden;
	border: 1px solid #eee;
	margin-bottom: 20rpx;
}
.list-con01-tab{
	display: flex;
	width: 100%;
	justify-content: flex-end;
}
.list-con01-tab text{
	width: 60rpx;
	padding: 10rpx 10rpx;
	text-align: center;
	font-size: 24rpx;
	color: #E5252A;
	background: #ffe5e5;
	border-radius: 40rpx 0 0 40rpx;
}
.list-con01-cent01{
	padding: 0 20rpx 30rpx 20rpx;
	width: calc( 100% - 40rpx );
	height: auto;
	font-size: 30rpx;
	color: #0C101C;
	text-align: left;
}
.list-con01-cent02{
	padding: 0 20rpx;
	width: calc( 100% - 40rpx );
	align-items: center;
}
.list-con01-cent02 text{
	padding-right: 30rpx;
	font-size: 26rpx;
	color: #9A9DA3;
}
.list-con-btn{
	width: 150rpx;
	height: 54rpx;
	line-height: 54rpx;
	text-align: center;
	border: 1rpx solid #E5252A;
	font-size: 24rpx;
	color: #E5252A;
	border-radius: 40rpx;
	background: #fff !important;
}
</style>

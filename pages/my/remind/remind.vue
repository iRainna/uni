<template>
	<view>
		<view v-if="!isDuanWang">
			<view class="remind-tit">
				<view class="remind-tit-con" @click="selDate">
					<text>选择时间</text>
					<image :src="isDate?'../../../static/image/Combo_a.png':'../../../static/image/Combo_aa.png'"></image>
				</view>
				<view class="remind-tit-con">
					<text>选择分类</text>
					<image src="../../../static/image/classification.png"></image>
				</view>
			</view>
			
			<view class="remind-con01">
				<view class="remind-con-bg">
					<view class="remind-con-bg02">
						<view class="remind-con-ctxt01">距离考试还有</view>
						<view class="remind-con-ctxt02">
							<text class="remind-ct01">15</text>
							<text>天</text>
						</view>
						<view class="remind-con-ctxt03">
							<text>当前分类:分类3</text>
						</view>
					</view>
				</view>
			</view>
			<view class="remind-con-tit">精选内容</view>
			<view class="remind-con01">
				<view class="remind-cent">
					<text>备考经验</text>
					<text>考试报名</text>
					<text>准考证打印</text>
					<text>成绩查询</text>
					<text>历年真题</text>
					<text>学员心声</text>
				</view>
				<view class="remind-cen-list">
					<view class="remind-list-tab">
						<text :class="tab==1?'remind-li-nav':''" @click="selTab(1)">热点</text>
						<text :class="tab==2?'remind-li-nav':''" @click="selTab(2)">及时</text>
						<text :class="tab==3?'remind-li-nav':''" @click="selTab(3)">免费资料</text>
					</view>
					<view class="remind-list-con">
						<view class="list-con-txt" v-for="(item,index) in list" :key='index'>{{item.cont}}</view>
					</view>
					<view class="remind-list-more">
						<text>查看更多</text>
						<image src="../../../static/image/more.png"></image>
					</view>
				</view>
			</view>
		</view>
		<view class="popup"  v-show="isDate">
			<view class="remind-popup animated fadeIn">
				<view class="remind-pop-tit">
					<view class="remind-tit-time">已选择{{year}}年{{month}}月{{day}}日</view>
				</view>
				<picker-view v-if="visible" class="remind-pop-date" :value="value" @change="bindChange">
					<picker-view-column>
						<view class="date-item" v-for="(item,index) in years" :key="index">{{item}}年</view>
					</picker-view-column>
					<picker-view-column>
						<view class="date-item" v-for="(item,index) in months" :key="index">{{item}}月</view>
					</picker-view-column>
					<picker-view-column>
						<view class="date-item" v-for="(item,index) in days" :key="index">{{item}}日</view>
					</picker-view-column>
				</picker-view>
				<button class="remind-pop-btn" hover-class="none" @click="selDate">确定</button>
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
			const date = new Date()
			const years = []
			const year = date.getFullYear()
			const months = []
			const month = date.getMonth() + 1
			const days = []
			const day = date.getDate()
			for (let i = 1990; i <= date.getFullYear(); i++) {
				years.push(i)
			}
			for (let i = 1; i <= 12; i++) {
				months.push(i)
			}
			for (let i = 1; i <= 31; i++) {
				days.push(i)
			}
			return {
				/* 选择日期 */
				isDate:false,
				title: 'picker-view',
				years,
				year,
				months,
				month,
				days,
				day,
				value: [9999, month - 1, day - 1],
				visible: true,
				// 断网：
				isDuanWang: false,
				tab:1,
				list:[
					{
						cont:'四川省2019下半年翻译资格考试成绩公示公示报告公示报告公示报告'
					},
					{
						cont:'黑龙江2019下半年翻译资格考试成绩公示报告公示报告公示报告公示报告公示报告'
					},
					{
						cont:'四川省2019下半年翻译资格考试成绩公示公示报告公示报告公示报告公示报告'
					},
					{
						cont:'四川省2019下半年翻译资格考试成绩公示公示报告公示报告公示报告公示报告'
					},
					{
						cont:'四川省2019下半年翻译资格考试成绩公示公示报告公示报告公示报告公示报告'
					},
					{
						cont:'四川省2019下半年翻译资格考试成绩公示公示报告公示报告公示报告公示报告'
					},
					{
						cont:'四川省2019下半年翻译资格考试成绩公示公示报告公示报告公示报告'
					},
					{
						cont:'四川省2019下半年翻译资格考试成绩公示公示报告'
					},
					{
						cont:'四川省2019下半年翻译资格考试成绩公示公示报告'
					},
					{
						cont:'四川省2019下半年翻译资格考试成绩公示公示报告'
					},
					{
						cont:'四川省2019下半年翻译资格考试成绩公示公示报告'
					}
				]
			}
		},
		methods: {
			selDate(){
				this.isDate = !this.isDate
			},
			/* 分类 */
			goClass(){
				uni.navigateTo({
					url:'/pages/index/intention/intention'
				})
			},
			/* 切换 */
			selTab(id){
				this.tab = id
			},
			/* 选择时间 */
			bindChange: function (e) {
				const val = e.detail.value
				this.year = this.years[val[0]]
				this.month = this.months[val[1]]
				this.day = this.days[val[2]]
			}
		}
	}
</script>

<style>
page{
	background: #F7F7F7;
}
.remind-con01{
	padding: 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	background: #fff;
	overflow: hidden;
}
.remind-tit{
	padding: 30rpx 0;
	width: 100%;
	height: auto;
	display: flex;
	align-items: center;
	overflow: hidden;
	position: fixed;
	background: #fff;
	z-index: 12;
}
.remind-tit-con{
	display: flex;
	align-items: flex-end;
	padding: 0 30rpx;
}
.remind-tit-con text{
	font-size: 28rpx;
	color: #0C101C;
}
.remind-tit-con image{
	width: 20rpx;
	height: 20rpx;
	display: block;
}
.remind-con-bg{
	margin-top: 90rpx;
	width: 100%;
	height: auto;
	overflow: hidden;
	background-image: linear-gradient(to bottom, #f43d46 , #ef4869) !important;
	border-radius: 10rpx;
}
.remind-con-bg02{
	padding: 30rpx 0;
	width: 100%;
	background: url(../../../static/image/spot.png) no-repeat;
	background-size: 100%;
}
.remind-con-ctxt01{
	width: 100%;
	font-size: 28rpx;
	color: #f9b0b4;
	text-align: center;
}
.remind-con-ctxt02{
	padding: 30rpx 0;
	width: 100%;
	font-size: 28rpx;
	color: #f9b0b4;
	display: flex;
	justify-content: center;
	align-items: baseline;
}
.remind-con-ctxt02 .remind-ct01{
	padding-right: 20rpx;
	font-size: 70rpx;
	color: #fff;
	font-weight: bold;
	display: block;
}
.remind-con-ctxt03{
	width: 100%;
	display: flex;
	justify-content: center;
}
.remind-con-ctxt03 text{
	padding: 10rpx 30rpx;
	font-size: 28rpx;
	color: #fff;
	background: #f36b81;
	border-radius: 40rpx;
}
.remind-con-tit{
	padding: 30rpx;
	width: calc( 100% - 60rpx );
	font-size: 32rpx;
	color: #0C101C;
	font-weight: bold;
}
.remind-cent{
	width: 100%;
	height: auto;
	overflow: hidden;
	border-bottom: 1px solid #eee;
	display: flex;
	flex-wrap: wrap;
	padding: 10rpx 0;
}
.remind-cent text{
	padding-left: 10rpx;
	width: calc( ( 100% - 30rpx ) / 3 );
	text-align: left;
	font-size: 28rpx;
	color: #0C101C;
	position: relative;
	margin-bottom: 30rpx;
}
.remind-cent text::after{
	content: '';
	position: absolute;
	width: 4rpx;
	height: 20rpx;
	background: #E5252A;
	border-radius: 30rpx;
	left: 0;
	top: 50%;
	margin-top: -10rpx;
}
.remind-cen-list{
	width: 100%;
	height: auto;
	overflow: hidden;
}
.remind-list-tab{
	padding: 30rpx;
	width: calc(100% - 60rpx);
	height: auto;
	display: flex;
}
.remind-list-tab text{
	width: calc( 100% / 3 );
	text-align: center;
	font-size: 30rpx;
	color: #9A9DA3;
	position: relative;
}
.remind-list-tab text::after{
	content: '';
	position: absolute;
	width: 20rpx;
	height: 7rpx;
	background: #fff;
	border-radius: 30rpx;
	left: 50%;
	margin-left: -10rpx;
	bottom: 0;
	margin-bottom: -16rpx;
}
.remind-list-tab .remind-li-nav{
	color: #0C101C;
	font-weight: bold;
}
.remind-list-tab .remind-li-nav::after {
	background-color: #0C101C;
}
.remind-list-con{
	padding:30rpx;
	width: calc( 100% - 60rpx );
	height: 400rpx;
	overflow: hidden;
}
.list-con-txt{
	margin-bottom: 20rpx;
	width: 100%;
	height: 35rpx;
	font-size: 26rpx;
	color:#0C101C;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
}
.remind-list-more{
	margin-top: 10rpx;
	width: 100%;
	display: flex;
	align-items: center;
}
.remind-list-more text{
	padding-left: 30rpx;
	font-size: 28rpx;
	color: #9A9DA3;
}
.remind-list-more image{
	margin-left: 15rpx;
	width: 20rpx;
	height: 20rpx;
	display: block;
}
.remind-popup{
	padding: 30rpx 0;
	width: 100%;
	height: 500rpx;
	position: fixed;
	z-index: 0;
	top:0;
	left: 0;
	background: #FFFFFF;
	margin-top: 160rpx;
}
.remind-pop-date{
	padding: 0 60rpx;
	width: calc( 100% - 120rpx );
	height: 300rpx;
}
.date-item{
	font-size: 28rpx;
	color: #0C101C;
	text-align: center;
	line-height: 60rpx;
}
.remind-pop-tit{
	width: 100%;
	height: 70rpx;
}
.remind-tit-time{
	width: 100%;
	text-align: center;
	font-size: 28rpx;
	color: #9A9DA3;
}
.remind-pop-btn{
	margin: 30rpx auto 0 auto;
	width: 255rpx;
	height: 90rpx;
	text-align: center;
	line-height: 90rpx;
	border-radius: 10rpx;
	font-size: 28rpx;
	color: #fff;
	background-image: linear-gradient(to right, #e83035 , #fa7174) !important;
}
</style>

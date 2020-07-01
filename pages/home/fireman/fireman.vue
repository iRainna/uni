<template>
	<view class="fireman">
		<view class="fireman_tab">
			<view v-if="!flag" class="tab_text" @click="showOrHide(flag,'flag')">
				<text>课程</text>
			</view>
			<view v-if="flag" class="tab_text2" @click="showOrHide(flag,'flag')">
				<text>课程</text>
			</view>
			<view v-if="!flag2" class="tab_text" @click="showOrHide(flag2,'flag2')">
				<text>直播</text>
			</view>
			<view v-if="flag2" class="tab_text2" @click="showOrHide(flag2,'flag2')">
				<text>直播</text>
			</view>
			<view v-if="!flag3" class="tab_text" @click="showOrHide(flag3,'flag3')">
				<text>题库</text>
			</view>
			<view v-if="flag3" class="tab_text2" @click="showOrHide(flag3,'flag3')">
				<text>题库</text>
			</view>
		</view>

		<view v-if="flag">
			<view class="zhiBo hot">
				<!-- <view class="zhiBo_head float zhong">
					<text>近期热门</text>
			
				</view> -->
				<view class="bookList">
					<view class="hotitem" v-for="(obj,i) in hot">
						<text class="hotTitle"><text class="hotTitleSp">{{obj.title1}}</text>{{obj.title2}}</text>
						<view v-for="(item,i) in obj.keywordList" class="keyword">{{item}}</view><br />
						<view class="t_bt">
						<view v-for="(obj,i) in obj.teacherList" class="hot_teacher">
							<image :src="obj.teacherimg" class="hot_t_img" mode=""></image>
						</view>
						<br />
						<view v-for="(obj,i) in obj.teacherList" class="hot_teacher">
							<text class="hot_name">{{obj.name}}</text>
						</view>

						<view class="teacher_rightbox">


							<!-- 正常 -->
							<view class="hotvalue" v-if="obj.isFalg == 1">
								<text class="v1css">￥{{obj.oldValue}} <text class="v1css2">起</text></text><br />
							</view>
							<!-- 免费 -->
							<view class="hotvalue" v-else-if="obj.isFalg == 2">
								<text class="hotfree">{{obj.free}}</text><br />
							</view>
							<!-- 现价和原价 -->
							<view class="hotvalue" v-else-if="obj.isFalg == 3">
								<text class="v1css">￥{{obj.newValue}} </text>
								<text class="hotoldv">￥{{obj.oldValue}} <text>起</text></text><br />
							</view>


							<view class="hotvalue" v-if="obj.isFalg == 1 || obj.isFalg == 2">
								<text class="v3css">10523人已抢</text>
							</view>

							<view class="hotvalue" v-if="obj.isFalg == 3">
								<text class="v3css">剩<text class="hotred">1</text>天 <text class="hotred">20:19:18</text>恢复原价</text>
							</view>
						</view>
</view>

						<text class="qiang" v-if="obj.isFalg == 2">免费</text>
						<text class="qiang" v-if="obj.isFalg == 3">限时抢购</text>
					</view>

				</view>
			</view>
		</view>
		<view v-if="flag2">
			<view class="zhiBo hot">
				<!-- <view class="zhiBo_head float zhong">
					<text>近期热门</text>
			
				</view> -->
				<view class="bookList">
					<view class="hotitem2 tikuItem2" v-for="(obj,i) in liveList">

						<view class="s2_title">
							{{obj.title}}
						</view>
						<view class="s2_user">
							<image :src="obj.user.img" mode=""></image><br />
							<text>{{obj.user.name}}</text>
						</view>
						<view class="sp_p">
							<view v-for="(obj2,i) in obj.list">
								<text class="fire_spText">{{obj2}}</text>
							</view>
							<view v-for="(obj3,i) in obj.free">
								<text class="fire_spText fire_spText2">{{obj3}}</text>
							</view>
						</view>
						<view class="f2_bottom">
							<view class="left">
								<view class="left1"  v-if="obj.flag==1">
									<image src="../../../static/zbGif.gif" class="left1Img" mode=""></image>
									<text>直播中</text>
								</view>
								<view class="left2"  v-if="obj.flag==2">
									<text>3月19日 19:30~21.30</text>
								</view>
							</view>
							<view class="right">
								<text class="r_text">{{obj.personNumber}}人&nbsp;&nbsp;已预约
								</text>
								<button v-if="obj.flag==1" class="appointment" @click="changestate(user,user.state)">进入直播</button>
								<button v-if="obj.flag==2" class="appointment" @click="changestate(user,user.state)">立即预约</button>
							</view>
						</view>

					</view>

				</view>
			</view>

		</view>
		<view v-if="flag3">
			<view class="zhiBo hot">
				<view class="tiku">
					<text>精选题库</text>
				</view>
				<view class="tikuItem" v-for="(item,i) in tiku">
					<view class="left">
						<text>{{item}}</text>
					</view>
					<view class="right">
						<text>去做题&gt;</text>
					</view>
				</view>
			</view>
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
				flag: true,
				flag2: false,
				flag3: false,
				hot: [{
						isFalg: 1,
						title1: '一级造价工程师',
						title2: '2020年临床执业医师-考点专项公开课 （直播+录播）',
						keywordList: ['性价比之选', '高效', '共55课次', '人气讲师团队'],
						teacherList: [{
							teacherimg: '../../../static/image/home_teacher_e.png',
							name: '王树京'
						}, {
							teacherimg: '../../../static/image/home_teacher_f.png',
							name: '陈明'
						}, {
							teacherimg: '../../../static/image/home_teacher_h.png',
							name: '肖国祥'
						}],
						state: 'normal',
						oldValue: 190,
						newValue: '',
						free: '免费'
					}, {
						isFalg: 2,
						title1: '一级造价工程师',
						title2: '2020年临床执业医师-考点专项公开课 （直播+录播）',
						keywordList: ['性价比之选', '高效', '共55课次', '人气讲师团队'],
						teacherList: [{
							teacherimg: '../../../static/image/home_teacher_e.png',
							name: '王树京'
						}, {
							teacherimg: '../../../static/image/home_teacher_f.png',
							name: '陈明'
						}, {
							teacherimg: '../../../static/image/home_teacher_h.png',
							name: '肖国祥'
						}],
						state: 'free',
						oldValue: '',
						newValue: '',
						free: '免费'
					},

					{
						isFalg: 3,
						title1: '一级造价工程师',
						title2: '2020年临床执业医师-考点专项公开课 （直播+录播）',
						keywordList: ['性价比之选', '高效', '共55课次', '人气讲师团队'],
						teacherList: [{
							teacherimg: '../../../static/image/home_teacher_e.png',
							name: '王树京'
						}, {
							teacherimg: '../../../static/image/home_teacher_f.png',
							name: '陈明'
						}, {
							teacherimg: '../../../static/image/home_teacher_h.png',
							name: '肖国祥'
						}],
						state: 'limitTime',
						oldValue: 4590,
						newValue: 3690,
						free: '免费'
					}
				],
				tiku: ['模拟考试', '历年真题', '考前押题', '习题记录', '我的错题', '我的笔记'],
				liveList: [{
					title: '专家解读课程名称专家解读课程名称专家解读课程名称',
					list: ['性价比之选', '高效学习', '共55课次'],
					free: ['免费'],
					flag: 1,
					personNumber: 10523,
					user: {
						name: '肖国祥',
						img: '../../../static/image/home_teacher_h.png'
					}
				},{
					title: '专家解读课程名称专家解读课程名称专家解读课程名称',
					list: ['性价比之选', '高效学习', '共55课次'],
					free: ['免费'],
					flag: 2,
					personNumber: 10523,
					user: {
						name: '肖国祥',
						img: '../../../static/image/home_teacher_h.png'
					}
				},{
					title: '专家解读课程名称专家解读课程名称专家解读课程名称',
					list: ['性价比之选', '高效学习', '共55课次'],
					free: ['免费'],
					flag: 2,
					personNumber: 10523,
					user: {
						name: '肖国祥',
						img: '../../../static/image/home_teacher_h.png'
					}
				}]
			}
		},
		methods: {
			showOrHide(parm1, parm2) {
				if (parm1 == false) {
					if (parm2 == 'flag') {
						this.flag = true;
						this.flag2 = false;
						this.flag3 = false;
					} else if (parm2 == 'flag2') {
						this.flag2 = true;
						this.flag = false;
						this.flag3 = false;
					} else if (parm2 == 'flag3') {
						this.flag3 = true;
						this.flag = false;
						this.flag2 = false;
					}
				}
			}
		}
	}
</script>

<style>
	page{
		background: rgb(247, 247, 247)
	}
	.left1 text,.left2 text{
		color: rgb(229, 37, 42);
		font-size: 24rpx;position: relative;
		top: -4rpx;
		
	}
	.left1 text{
		margin-left: 10rpx;
	}
	.right text{
		color: rgb(171, 177, 184);
		color: rgb(0, 0, 0);
		font-size: 28rpx;
		position: relative;
		/* left: -110rpx; */
		top: -10rpx;
	}
	.fireman {
		background-color: rgb(247, 247, 247);
	}

	.fireman_tab {
		position: fixed;
		width: 100%;
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
background: white;
    padding-bottom: 40rpx;
	}

	.tab_text {
		margin-left: 45rpx;
		margin-right: 45rpx;
		font-size: 30rpx;
		color: rgb(154, 157, 163);
	}

	.tab_text2 {
		margin-left: 45rpx;
		margin-right: 45rpx;
		font-size: 30rpx;
		color: rgb(0, 0, 0);
		font-weight: bold;
	}

	.tab_text2::after {
		content: '';
		width: 18rpx;
		height: 4rpx;
		border-radius: 4rpx;
		background-color: #000000;
		position: absolute;
		margin-top: 48rpx;
		margin-left: -40rpx;
	}

	,

	.zhiBo {
		overflow: hidden;
		padding-left: 30rpx;
		padding-right: 30rpx;
		/* padding-top: 37rpx; */
		padding-bottom: 37rpx;
		border-bottom: solid 30rpx #f7f7f7;
	}

	.hot {
		background: #f7f7f7;
	}

	.bookList {
		display: flex;
		width: 100%;
		height: auto;
		/* background-color: #07B666; */
		flex-wrap: wrap;
		flex-direction: row;
		justify-content: space-around;
		margin-top: 100rpx;
	}

	.bookitem {
		width: 210rpx;
		height: 300rpx;
		/* background-color: #007AFF; */
		margin-left: 10rpx;
		margin-right: 10rpx;
		text-align: center;
	}

	.bookimg {
		width: 170rpx;
		height: 200rpx;
		display: inline-block;
	}

	.tea_imgbox {
		width: 210rpx;
		height: 210rpx;
	}

	.teacherimg {
		width: 160rpx;
		height: 180rpx;
		position: relative;
		bottom: -34rpx;
	}

	.bookmsg {
		width: 210rpx;
		font-size: 24rpx;
		margin-top: 20rpx;
		text-align: center;
		line-height: 40rpx;
		display: block;
	}

	.tea_imgbox {
		background-color: rgb(231, 231, 240);
	}

	.teacher_level {
		color: rgb(154, 156, 164);
		/* position: relative;
		top: -8rpx; */
	}

	.hot {
		background: #f7f7f7;
	}

	.hotitem {
		width: 690rpx;
		height: 390rpx;
		background-color: white;
		margin-top: 0rpx;
		margin-bottom: 20rpx;
		padding-left: 20rpx;
	}

	.hotTitle {
		/* padding-left: 20rpx; */
		height: 60rpx;
		display: inline-flex;
		margin: 0 auto;
		text-align: left;
		font-size: 32rpx;
		margin-top: 52rpx;
		line-height: 48rpx;
	}

	.hotTitleSp {
		background-color: rgb(132, 140, 148);
		color: white;
		font-size: 24rpx;
		padding-left: 10rpx;
		padding-top: 3rpx;
		padding-right: 10rpx;
		padding-bottom: 3rpx;
		border-radius: 5rpx;
		margin-right: 30rpx;
		margin-left: 6rpx;
	}

	.keyword {
		font-size: 24rpx;
		display: inline-flex;
		background-color: rgb(247, 247, 247);
		color: rgb(172, 183, 189);
		margin-left: 6rpx;
		margin-right: 6rpx;
		padding-left: 16rpx;
		padding-right: 16rpx;
		padding-bottom: 6rpx;
		padding-top: 6rpx;
		border-radius: 5rpx;
		margin-top: 20rpx;
		justify-content: center;
			position: relative;
			    top: 40rpx;}

	.hot_t_img {
		width: 67rpx;
		height: 67rpx;
		background-color: white;
	}

	.hot_teacher {
		display: inline-flex;
		width: 80rpx;
		position: relative;
		top: 40rpx;
	}

	.hot_teacher:nth(2) {
		display: inline-flex;
		width: 150rpx;
		position: relative;
		top: 40rpx;
		left: 30rpx;
	}

	.hot_name {
		display: inline-block;
		font-size: 24rpx;
		position: relative;
		/* top: 44px; */
		width: 80rpx;
		text-align: center;
		left: -6rpx;
	}

	/* .dipon{
		display: block !important;
	}
	.disnone{
		display: none !important;
	} */
	.hotvalue {
		display: flex;
		justify-content: flex-end;
		margin-right: 30rpx;
		margin-right: 56rpx;
		    line-height: 60rpx;
		    margin-top: -24rpx;
			    margin-bottom: 16rpx;
	}

	.v1css {
		font-size: 35rpx;
		color: rgb(233, 34, 41);
	}

	.v1css2 {
		font-size: 24rpx;
		color: rgb(165, 165, 167);
		/* 108 116 131 */
	}

	.v3css {
		color: rgb(108, 116, 131);
		font-size: 24rpx;
	}

	.hotfree {
		color: rgb(1, 181, 99);
	}

	.hotoldv {
		color: rgb(131, 131, 136);
		font-size: 24rpx;
		text-align: center;
		line-height: 60rpx;
		text-decoration: line-through;
	}

	/* .hotoldv::after {
		content: '';
		position: absolute;
		width: 52rpx;
		height: 1rpx;
		right: 90rpx;
		margin-top: 34rpx;
		background-color: rgb(131, 131, 136);
	}
 */
	.hotred {
		color: rgb(233, 34, 41);
	}
	.qiang{
		color: white;
		font-size: 24rpx;
		background-color: rgb(249,76,83);
		border-bottom-left-radius:10rpx ;
			border-bottom-right-radius:10rpx ;
			padding-left: 24rpx;
			padding-top: 2rpx;
			padding-right: 24rpx;
			padding-bottom: 2rpx;
			position: relative;
			    top: -418rpx;
			    left: 500rpx;
	}
	.teacher_rightbox{
		position: relative;
		    top: -48rpx;
	}
	.t_bt{
		position: relative;
		top: 30rpx;
	}

	.teacher_rightbox{
		position: relative;
		    top: -48rpx;
	}

	.tiku {
		font-size: 34rpx;
		font-weight: bold;
		margin-bottom: 40rpx;
		margin-top: 110rpx;
	}

	.tikuItem2 {
		display: inline-flex;
		width: 88.5%;
		;
		background-color: white;
		margin-top: 10rpx;
		margin-bottom: 10rpx;
		padding-left: 28rpx;
		padding-top: 32rpx;
		padding-right: 28rpx;
		padding-bottom: 32rpx;
		flex-wrap: wrap;
		/* border: solid 16rpx rgb(247,247,247); */
	}

	.tikuItem {
		display: inline-flex;
		width: 100%;
		background-color: white;
		margin-top: 10rpx;
		margin-bottom: 10rpx;
		padding-left: 28rpx;
		padding-top: 32rpx;
		padding-right: 28rpx;
		padding-bottom: 32rpx;

	}


	.left {
		width: 50%;
		font-size: 32rpx;
	}

	.right {
		width: 50%;
		font-size: 32rpx;
		text-align: right;
		padding-right: 60rpx;
		position: relative;
		top: 8rpx;
	}

	.s2_title {
		width: 480rpx;
		height: 95rpx;
		font-size: 32rpx;
		line-height: 50rpx;
	}

	.s2_user {
		width: 127rpx;
		text-align: center;
		height: 140rpx;
	}

	.s2_user image {
		width: 68rpx;
		height: 68rpx;
		display: inline-block;
	}

	.s2_user text {
		font-size: 24rpx;
		color: rgb(140, 145, 168);
		position: relative;
		top: -10rpx;
	}

	.fire_spText {
		background-color: rgb(245, 247, 251);
		color: rgb(171, 177, 184);
		font-size: 24rpx;
		padding-left: 18rpx;
		padding-top: 7rpx;
		padding-bottom: 7rpx;
		padding-right: 18rpx;
		margin-left: 6rpx;
		margin-right: 6rpx;
	}

	.fire_spText2 {
		background-color: rgb(245, 247, 251);
		color: rgb(171, 177, 184);
		font-size: 24rpx;
		padding-left: 18rpx;
		padding-top: 7rpx;
		padding-bottom: 7rpx;
		padding-right: 18rpx;
		margin-left: 6rpx;
		margin-right: 6rpx;
		background-color: rgb(205, 240, 224);
		color: rgb(98, 201, 147);
	}

	.sp_p {
		display: inline-flex;
		flex-wrap: wrap;
		position: relative;
		top: -10rpx;
	}

	.left1Img {
		width: 38rpx;
		height: 38rpx;
	}

	.f2_bottom {
		width: 100%;
		display: inline-flex;
		flex-wrap: nowrap;
		position: relative;
		top: 50rpx;
	}

	.appointment {
		width: 150rpx;
		height: 64rpx;
		font-size: 24rpx;
		background: linear-gradient(to right, rgb(191, 72, 85) 0%, rgb(248, 115, 83) 100%);
		background-color: ;
		line-height: 44rpx;
		color: white;
		border-radius: 44rpx;
		padding-left: 25rpx;
		padding-right: 25rpx;
		padding-bottom: 10rpx;
		padding-top: 10rpx;
		position: relative;
		left: 200rpx;
		bottom: 60rpx;
	}
	.r_text{
		    color: rgb(171, 177, 184) !important;
		    /* color: rgb(0, 0, 0); */
		    font-size: 28rpx;
		    position: relative;
		    left: -84rpx;
		    top: -10rpx;
	}
</style>

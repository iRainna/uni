<template>
	<view class="home">
		<!-- header -->
		<view class="header float zhong">
			<view class="header_left " @tap="goTo119">
				<text>初级消防员</text>
				<image src="../../static/image/classification.png" mode=""></image>
			</view>
			<view class="header_right" @tap="goSearch()">
				<image src="../../static/image/search.png" mode=""></image>
			</view>
		</view>


		<!-- banner -->
		<view class="banner">
			<swiper class="banner_swiper" :indicator-dots="indicatorDots" indicator-active-color="#cf9b0e" :autoplay="autoplay"
			 :interval="interval" :duration="duration">
				<swiper-item v-for="(item, index) in bannerList" :key="index">
					<view class="banner_li">
						<image :src="item.Image" mode=""></image>
					</view>
				</swiper-item>
			</swiper>
		</view>

		<!-- 福利大放送 -->
		<view class="fuLi" @tap="goActivity">
			<image src="../../static/image/banner_fu.png" mode=""></image>
		</view>

		<!-- 建筑师 -->
		<view class="jian">
			<swiper class="jian_swiper" :indicator-dots="indicatorDotsa" indicator-active-color="#171917" :autoplay="autoplaya"
			 :interval="intervala" :duration="durationa">
				<swiper-item v-for="(item, index) in bannerList" :key="index">
					<view class="jian_li">
						<text v-for="(item,index) in textList" :key='index'>{{ item.text }}</text>
					</view>
				</swiper-item>
			</swiper>
		</view>

		<!-- 直播 -->
		<view class="zhiBo">
			<view class="zhiBo_head float zhong">
				<text>直播</text>
				<view class="zhiBo_fg zhong">
					<text>更多</text>
					<image src="../../static/image/home_more.png" mode=""></image>
				</view>
			</view>
			<view class="zhiBo_list" :class="isLiheight?'autoHeight':''">

				<view v-for="(user,i) in listObj" class="zhiBo_li float ">
					<view class="zhiBo_hg">
						<view class="zhiBo_h6">{{user.time}}</view>
						<text>{{user.date}}</text>
						<image src="../../static/image/hb.png" mode=""></image>
					</view>
					<view class="zhiBo_right">
						<view class="zhiBo_div">
							<text class="zhibo_title">
								<text class="zhibo_title1">{{user.title1}}</text>
								{{user.title2}}
							</text>
							<view class="zhibo_box">
								<image :src="user.imgurl" class="zhiboteacher_img" mode=""></image>
								<text class="teachername">讲师&nbsp;&nbsp;&nbsp;{{user.name}} </text>
								<text class="personNumber">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{{user.personNumble}}人</text>
								<text v-if="user.state" class="zhibo_text">已预约</text>
								<button v-if="!user.state" class="appointment" hover-class="none" @click="changestate(user,user.state)">马上预约</button>
							</view>
						</view>
					</view>
				</view>
				<view class="openView" @tap="isLiheight=!isLiheight" v-if="!isLiheight">
					<text class="open">展开近期直播</text>
					<image src="../../static/image/more.png" class="openmore" mode=""></image>
				</view>
				<view class="openView" @tap="isLiheight=!isLiheight" v-if="isLiheight">
					<text class="open">收起近期直播</text>
					<image src="../../static/image/more.png" class="openmore2" mode=""></image>
				</view>
			</view>
		</view>

		<!-- 图书 -->
		<view class="zhiBo">
			<view class="zhiBo_head float zhong">
				<text>图书</text>
				<view class="zhiBo_fg zhong">
					<text>更多</text>
					<image src="../../static/image/home_more.png" mode=""></image>
				</view>
			</view>
			<view class="bookList">
				<view class="bookitem" v-for="(obj,i) in book">
					<image :src="obj.bookimgurl" class="bookimg" mode=""></image><br />
					<text class="bookmsg">{{obj.bookmsg}}</text>
				</view>

			</view>
		</view>

		<!-- 网校名师 -->
		<view class="zhiBo">
			<view class="zhiBo_head float zhong">
				<text>网校名师</text>
				<view class="zhiBo_fg zhong">
					<text>更多</text>
					<image src="../../static/image/home_more.png" mode=""></image>
				</view>
			</view>
			<view class="bookList">
				<view class="bookitem" v-for="(obj,i) in teachers">
					<view class="tea_imgbox">
						<image :src="obj.teacherImgurl" class="bookimg teacherimg " mode=""></image>
					</view>

					<text class="bookmsg">{{obj.name}}
						<br />
						<text class="teacher_level">
							{{obj.level}}
						</text>

					</text>
					
				</view>
    
			</view>
		</view>

		<!-- 近期热门 -->
		<view class="zhiBo hot">
			<view class="zhiBo_head float zhong">
				<text>近期热门</text>

			</view>
			<view class="bookList">
				<view class="hotitem" v-for="(obj,i) in hot">
					<text class="hotTitle"><text class="hotTitleSp">{{obj.title1}}</text>{{obj.title2}}</text>
					<view class="keyword_box">
						
				
					<view v-for="(item,i) in obj.keywordList" class="keyword">{{item}}</view>
						</view>
					<view class="t_bt">
						<view class="flex">
							<view v-for="(obj,i) in obj.teacherList" :key='i' class="flex imgAndname">
								<view class="hot_teacher">
									<image :src="obj.teacherimg" class="hot_t_img" mode=""></image>
								</view>
								<view class="hot_teacher">
									<text class="hot_name">{{obj.name}}</text>
								</view>
							</view>
						</view>
						<view class="teacher_rightbox">
							<!-- 正常 -->
							<view  class="hotvalue" v-if="obj.isFalg == 1">
								<text class="v1css">￥{{obj.oldValue}} <text class="v1css2">起</text></text>
							</view>
							<!-- 免费 -->
							<view  class="hotvalue" v-else-if="obj.isFalg == 2">
								<text class="hotfree">{{obj.free}}</text>
							</view>
							<!-- 现价和原价 -->
							<view class="hotvalue" v-else-if="obj.isFalg == 3">
								<text class="v1css">￥{{obj.newValue}} </text>
								<text class="hotoldv">￥{{obj.oldValue}} <text>起</text></text>
							</view>
							
							
							<view  class="hotvalue" v-if="obj.isFalg == 1 || obj.isFalg == 2">
								<text class="v3css">10523人已抢</text>
							</view>
							
							<view class="hotvalue" v-if="obj.isFalg == 3">
								<text class="v3css">剩<text class="hotred">1</text>天 <text class="hotred">20:19:18</text>恢复原价</text>
							</view>
						</view>
					
					</view>
					<text class="qiang" v-if="obj.isFalg == 2">免&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;费</text>
					<text class="qiang" v-if="obj.isFalg == 3">限时抢购</text>
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
				bannerList: [{
						Image: '../../static/image/banner.png'
					},
					{
						Image: '../../static/image/banner.png'
					},
					{
						Image: '../../static/image/banner.png'
					}
				],
				// textList
				indicatorDotsa: true,
				autoplaya: false,
				intervala: 2000,
				durationa: 500,
				textList: [{
						text: '一级建筑'
					},
					{
						text: '一级建筑'
					},
					{
						text: '一级建筑'
					},
					{
						text: '一级建筑'
					},
					{
						text: '一级建筑'
					},
					{
						text: '一级建筑'
					},
					{
						text: '一级建筑'
					},
					{
						text: '一级建筑'
					},
					{
						text: '一级建筑'
					}
				],
				listObj: [{
						time: '19:20',
						date: '3月18日',
						title1: '人力',
						title2: '倾力专项政策详细解读课程名称（上）',
						name: '张蓝',
						personNumble: 201,
						imgurl: '../../static/image/head.png',
						state: true
					}, {
						time: '19:20',
						date: '3月18日',
						title1: '人力',
						title2: '倾力专项政策详细解读课程名称（上）',
						name: '张蓝',
						personNumble: 201,
						imgurl: '../../static/image/head.png',
						state: true
					},
					{
						time: '19:20',
						date: '3月18日',
						title1: '人力',
						title2: '倾力专项政策详细解读课程名称（上）',
						name: '张蓝',
						personNumble: 201,
						imgurl: '../../static/image/head.png',
						state: true
					}, {
						time: '19:20',
						date: '3月18日',
						title1: '人力',
						title2: '倾力专项政策详细解读课程名称（上）',
						name: '张蓝',
						personNumble: 201,
						imgurl: '../../static/image/head.png',
						state: true
					},
					{
						time: '19:20',
						date: '3月18日',
						title1: '人力',
						title2: '倾力专项政策详细解读课程名称（上）',
						name: '张蓝',
						personNumble: 201,
						imgurl: '../../static/image/head.png',
						state: false
					},
					{
						time: '19:20',
						date: '3月18日',
						title1: '人力',
						title2: '倾力专项政策详细解读课程名称（上）',
						name: '张蓝',
						personNumble: 201,
						imgurl: '../../static/image/head.png',
						state: false
					}
				],

				book: [{
					bookimgurl: '../../static/image/book_b.png',
					bookmsg: '建筑工程法律法规相关知识'
				}, {
					bookimgurl: '../../static/image/book_b.png',
					bookmsg: '建筑工程法律法规相关知识'
				}, {
					bookimgurl: '../../static/image/book_b.png',
					bookmsg: '建筑工程法律法规相关知识'
				}, ],
				teachers: [{
					name: '张敏',
					teacherImgurl: '../../static/image/teacher_a.png',
					level: '二级建筑师'
				}, {
					name: '张敏',
					teacherImgurl: '../../static/image/teacher_b.png',
					level: '二级建筑师'
				}, {
					name: '张敏',
					teacherImgurl: '../../static/image/teacher_c.png',
					level: '二级建筑师'
				}],
				hot: [{
					isFalg:1,
						title1: '一级造价工程师',
						title2: '2020年临床执业医师-考点专项公开课 （直播+录播）',
						keywordList: ['性价比之选', '高效', '共55课次', '人气讲师团队'],
						teacherList: [{
							teacherimg: '../../static/image/home_teacher_e.png',
							name: '王树京'
						}, {
							teacherimg: '../../static/image/home_teacher_f.png',
							name: '陈明'
						}, {
							teacherimg: '../../static/image/home_teacher_h.png',
							name: '肖国祥'
						}],
						state: 'normal',
						oldValue: 190,
						newValue: '',
						free: '免费'
					}, {
						isFalg:2,
						title1: '一级造价工程师',
						title2: '2020年临床执业医师-考点专项公开课 （直播+录播）',
						keywordList: ['性价比之选', '高效', '共55课次', '人气讲师团队'],
						teacherList: [{
							teacherimg: '../../static/image/home_teacher_e.png',
							name: '王树京'
						}, {
							teacherimg: '../../static/image/home_teacher_f.png',
							name: '陈明'
						}, {
							teacherimg: '../../static/image/home_teacher_h.png',
							name: '肖国祥'
						}],
						state: 'free',
						oldValue: '',
						newValue: '',
						free: '免费'
					},

					{isFalg:3,
						title1: '一级造价工程师',
						title2: '2020年临床执业医师-考点专项公开课 （直播+录播）',
						keywordList: ['性价比之选', '高效', '共55课次', '人气讲师团队'],
						teacherList: [{
							teacherimg: '../../static/image/home_teacher_e.png',
							name: '王树京'
						}, {
							teacherimg: '../../static/image/home_teacher_f.png',
							name: '陈明'
						}, {
							teacherimg: '../../static/image/home_teacher_h.png',
							name: '肖国祥'
						}],
						state: 'limitTime',
						oldValue: 4590,
						newValue: 3690,
						free: '免费'
					}
				]
			};
		},

		methods: {
			// 骨架屏
			reloadData() {
				this.loading = true;
				setTimeout(() => {
					this.loading = false;
				}, 2000);
			},
			changestate(item, parm) {
				// console.log(parm);
				item.state = !parm;
				++item.personNumble
				// console.log(item);
			},
			goSearch(){
				uni.navigateTo({
				                    url: 'search/search',
				                    success: res => {},
				                    fail: () => {},
				                    complete: () => {}
				                });
			},
			goActivity(){
				uni.navigateTo({
				                    url: 'activity/activity',
				                    success: res => {},
				                    fail: () => {},
				                    complete: () => {}
				                });
			},
			goTo119(){
				uni.navigateTo({
				                    url: 'fireman/fireman',
				                    success: res => {},
				                    fail: () => {},
				                    complete: () => {}
				                });
			}
		}
	};
</script>

<style>
	.zhiBo_div {
		/* overflow: hidden; */
		padding-left: 27rpx;
		padding-right: 27rpx;
	}

	.zhiBo_right {
		overflow: hidden;
		width: calc(100% - 150rpx);
		background-color: #f7f7ff;
		padding-top: 30rpx;
		padding-bottom: 30rpx;
		margin-bottom: 30rpx;
	}

	.zhiBo_hg image {
		display: block;
		width: 27rpx;
		height: 27rpx;
		position: absolute;
		right: 0;
		top: 0;
		z-index: 10;
	}

	.zhiBo_hg text {
		font-size: 24rpx;
		color: #999;
		display: block;
		text-align: left;
		margin-top: 10rpx;
	}

	.zhiBo_h6 {
		font-size: 28rpx;
		color: #333;
		text-align: left;
	}

	.zhiBo_hg {
		overflow: hidden;
		width: 140rpx;
		position: relative;
	}

	.zhiBo_li {
		overflow: hidden;
		display: flex;
	}

	.zhiBo_list {
		overflow: hidden;
		    margin-top: 30rpx;
	}

	/* zhiBo_list */

	.zhiBo_head .zhiBo_fg image {
		display: block;
		width: 20rpx;
		height: 20rpx;
	}

	.zhiBo_head .zhiBo_fg text {
		font-size: 24rpx;
		color: #999;
		margin-right: 0.5em;

	}

	.zhiBo_head .zhiBo_fg {
		overflow: hidden;
		display: flex;
	}

	.zhiBo_head>text {
		font-size: 34rpx;
		color: #333;
		font-weight: 600;
	}

	.zhiBo_head {
		overflow: hidden;
		display: flex;
	}

	.zhiBo {
		overflow: hidden;
		padding-left: 30rpx;
		padding-right: 30rpx;
		padding-top: 37rpx;
		padding-bottom: 37rpx;
		border-bottom: solid 30rpx #f7f7f7;
	}

	/* zhiBo */

	.jian_li text {
		font-size: 24rpx;
		color: #333;
		background-color: #f7f7ff;
		height: 60rpx;
		line-height: 60rpx;
		padding-left: 20rpx;
		padding-right: 20rpx;
		display: inline-block;
		border-radius: 6rpx;
		margin-right: 15rpx;
		margin-left: 15rpx;
		margin-top: 15rpx;
	}

	.jian_li {
		overflow: hidden;
		height: 160rpx;
	}

	.jian_swiper {
		overflow: hidden;
		height: 200rpx;
	}

	.jian {
		overflow: hidden;
		padding-left: 30rpx;
		padding-right: 30rpx;
		padding-top: 40rpx;
		padding-bottom: 40rpx;
		border-bottom: solid 30rpx #f7f7f7;
	}

	/* jian */

	.fuLi image {
		display: block;
		width: 100%;
		height: 100%;
	}

	.fuLi {
		overflow: hidden;
		width: 716rpx;
		height: 172rpx;
		margin: 0 auto;
	}

	/* fuLi */

	.banner_swiper,
	.banner_li,
	.banner_li image {
		overflow: hidden;
		width: 100%;
		height: 310rpx;
	}

	.banner_li {
		background: url(../../static/image/banner_a.png) no-repeat left top;
		background-size: 100% 100%;
	}

	.banner {
		overflow: hidden;
		width: 100%;
		height: 310rpx;
		margin-top: 132rpx;
	}

	/* banner */

	.header_right image {
		display: block;
		width: 28rpx;
		height: 28rpx;
	}

	.header_right {
		overflow: hidden;
		display: flex;
		justify-content: flex-end;
	}

	.header_left image {
		display: block;
		width: 20rpx;
		height: 20rpx;
	}

	.header_left text {
		font-size: 28rpx;
		color: #333;
		margin-right: 0.5em;
	}

	.header_left {
		overflow: hidden;
		display: flex;
		align-items: flex-end;
	}

	.header {
		width: calc(100% - 60rpx);
		padding-left: 30rpx;
		padding-right: 30rpx;
		background-color: #fff;
		padding-top: 44rpx;
		height: 88rpx;
		display: flex;
		position: fixed;
		left: 0;
		top: 0;
		z-index: 50;
	}

	.home {
		overflow: hidden;
	}

	.zhibo_title1 {
		width: 75rpx;
		height: 20rpx;
		font-size: 24rpx;
		border-radius: 5rpx;
		line-height: 20rpx;
		text-align: center;
		padding-left: 18rpx;
		padding-right: 17rpx;
		padding-top: 2rpx;
		padding-bottom: 2rpx;
		margin-right: 18rpx;
		background-color: rgb(247, 247, 239);
		border: solid 1rpx rgb(246, 187, 111);
		color: rgb(246, 187, 111);
	}

	.zhibo_title {
		font-size: 32rpx;
		line-height: 50rpx
	}

	.zhiboteacher_img {
		width: 45rpx;
		height: 45rpx;
		position: relative;
		top: 10rpx;
	}

	.teachername {
		font-size: 24rpx;
		position: relative;
		left: 24rpx;
		color: rgb(108, 116, 131);
	}

	.personNumber {
		font-size: 24rpx;
		position: relative;
		right: -100rpx;
		color: rgb(108, 116, 131);
	}

	.zhibo_text {
		font-size: 22rpx;
		position: relative;
		right: -120rpx;
		color: rgb(108, 116, 131);
	}

	.appointment {
		width: 150rpx;
		height: 64rpx;
		font-size: 24rpx;
		background: linear-gradient(to right, #f94c53 0%, #f97287 100%) !important;
		background-color: ;
		line-height: 44rpx;
		color: white;
		border-radius: 44rpx;
		padding-left: 25rpx;
		padding-right: 25rpx;
		padding-bottom: 10rpx;
		padding-top: 10rpx;
		position: relative;
		left: 340rpx;
		bottom: 50rpx;
	}

	.zhibo_box {
		height: 80rpx;
		/* overflow: hidden; */
		position: relative;
		    top: 24rpx;
	}

	.zhiBo_li:nth(n+5) {
		display: none;
	}

	.autoHeight .zhiBo_li:nth(n+5) {
		display: block;
	}

	.open {
		color: rgb(156, 165, 167);
		font-size: 24rpx;
	}

	.openmore {
		width: 20rpx;
		height: 20rpx;
		transform: rotate(90deg);
		margin-left: 15rpx;
	}
	.openmore2 {
		width: 20rpx;
		height: 20rpx;
		transform: rotate(270deg);
		margin-left: 15rpx;
	}

	.openView {
		width: 220rpx;
		height: 60rpx;
		text-align: center;
		margin: 0 auto;
	}

	.bookList {
		display: flex;
		width: 100%;
		height: auto;
		/* background-color: #07B666; */
		flex-wrap: wrap;
		flex-direction: row;
		justify-content: space-around;
		margin-top: 40rpx;
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
		width: calc( 100% - 40rpx );
		
		height: 390rpx;
		background-color: white;
		margin-top: 0rpx;
		margin-bottom: 20rpx;
		padding-left: 20rpx;
			padding-right: 20rpx;
		position: relative;
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
			/* position: relative;
			    top: 40rpx; */
				}

	.hot_t_img {
		width: 67rpx;
		height: 67rpx;
		background-color: white;
	}

	.hot_teacher {
		display: inline-flex;
		width: 80rpx;
		/* position: relative;
		top: 40rpx; */
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
		   /* line-height: 60rpx;
		    margin-top: -24rpx;
			    margin-bottom: 16rpx; */
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
	    font-size: 12px;
	    background: linear-gradient(to right, #f94c53 0%, #f97287 100%);
	    border-bottom-left-radius: 5px;
	    border-bottom-right-radius: 5px;
	    padding-left: 12px;
	    padding-top: 1px;
	    padding-right: 12px;
	    padding-bottom: 1px;
	    position: absolute;
	    top: 0;
	    left: 250px;
	}
	.teacher_rightbox{
		display: flex;
		flex-direction: column;
		    top: -48rpx;
			    align-items: flex-end;
	}
	.t_bt{
		display: flex;
		top: 30rpx;
		align-items: center;
		    justify-content: space-between;
		
	}
	.keyword_box{
		display: inline-flex;
		align-items: center;
		margin-top: 40rpx;
		margin-bottom: 40rpx;
	}
	.imgAndname{
		flex-direction:column ;
	}
</style>

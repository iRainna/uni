<template>
	<view class="search">
		<!-- 搜索 -->
		<view class="fixed">
			<view class="header">
				<view class="header_p">


					<icon :type="searchicon" size="16" class="iconSearch" />
					<input type="text" value="" class="searchInput" placeholder="搜索考试名称、老师名称或课程名称" />
					<icon :type="clearicon" size="16" class="iconClear" />
					<text class="quxiao">取消</text>
				</view>
			</view>
		</view>
		<!-- 可以搜索到 -->
		<view v-if="true">
			<!-- 考试频道 -->
			<view class="test">
				<text class="testTitle">考试频道</text>
				<view v-for="(item,i) in test">
					<text class="testcontent">{{item}}</text>
				</view>
			</view>
			<!-- 课程 -->
			<view class="zhiBo hot">
				<view class="zhiBo_head float zhong">
					<text class="testTitle courseTitle">课程</text>

				</view>

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
		<!-- 搜索不到时 -->
		<view v-if="false" class="noSearch n1">
			<image src="../../../static/image/bg_a.png" class="noSearchImg" mode=""></image><br />

		</view>
		<view v-if="false" class="noSearch">
			<text class="noSearchText">你搜索的结果不存在~</text>
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
				searchicon: ['search'],
				clearicon: ['clear'],
				test: ['一级造价工程师'],
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
				]
			}
		},
		onLoad() {
			// #ifdef APP-PLUS|| MP-WEIXIN
			this.iconType = ['success', 'success_no_circle', 'info', 'warn', 'waiting', 'cancel', 'download', 'search', 'clear']
			// #endif
			// #ifdef MP-ALIPAY
			this.iconType = ['info', 'warn', 'waiting', 'cancel', 'download', 'search', 'clear', 'success', 'success_no_circle',
				'loading'
			]
			// #endif
			// #ifdef MP-BAIDU
			this.iconType = ['success', 'info', 'warn', 'waiting', 'success_no_circle', 'clear', 'search', 'personal', 'setting',
				'top', 'close', 'cancel', 'download', 'checkboxSelected', 'radioSelected', 'radioUnselect'
			]
			// #endif
		}

	}
</script>

<style>
	.fixed {
		width: 100vw;
		position: fixed;
		top: 0;
	}

	.header {
		position: fixed;
	}

	.header_p {
		position: relative;
		/* top: 30rpx; */
	}

	page {
		background: rgb(247, 247, 247)
	}

	.search {
		background-color: rgb(247, 247, 247);
		width: 100%;
		/* height: 100%; */
		height: 93.1vh;
		   
	}

	.search .header {
		height: 80rpx;
		background-color: white;
		text-align: center;
		position: relative;
		border-bottom: 2rpx solid rgb(237, 237, 238);
		 padding-top: 20px;
	}

	.searchInput {
		width: 500rpx;
		height: 60rpx;
		background-color: rgb(247, 247, 247);
		border-radius: 60rpx;
		display: inline-block;
		font-size: 24rpx
	}

	.iconSearch {
		position: absolute;
		left: 140rpx;
		top: 18rpx;
	}

	.iconClear {
		position: absolute;
		right: 140rpx;
		top: 18rpx;
	}

	.quxiao {
		font-size: 30rpx;
		color: rgb(108, 119, 129);
		position: absolute;
		right: 40rpx;
		top: 10rpx;

	}

	.search .test {
		height: 217rpx;
		width: 100%;
		background-color: white;
		padding-top: 20rpx;
		padding-left: 20rpx;
		margin-top: 124rpx;
	}

	.search .test .testTitle {
		color: rgb(155, 157, 163);
		font-size: 24rpx;
	}

	.search .test .testcontent {
		display: inline-flex;
		height: calc(100% - 30rpx);
		font-size: 36rpx;
		margin-top: 20rpx;
		line-height: 60rpx;
	}

	.courseTitle {
		color: rgb(155, 157, 163);
		font-size: 24rpx;
	}

	.zhiBo {
		overflow: hidden;
		padding-left: 30rpx;
		padding-right: 30rpx;
		padding-top: 37rpx;
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
		top: 40rpx;
	}

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

	.qiang {
		color: white;
		font-size: 24rpx;
		background-color: rgb(249, 76, 83);
		border-bottom-left-radius: 10rpx;
		border-bottom-right-radius: 10rpx;
		padding-left: 24rpx;
		padding-top: 2rpx;
		padding-right: 24rpx;
		padding-bottom: 2rpx;
		position: relative;
		top: -418rpx;
		left: 500rpx;
	}

	.teacher_rightbox {
		position: relative;
		top: -48rpx;
	}

	.t_bt {
		position: relative;
		top: 30rpx;
	}

	.noSearch {
		width: 100%;
		/* height: 64vh; */
		display: inline-flex;
		justify-content: center;
		/* padding-top: 150rpx; */
	}

	.n1 {
		margin-top: 10rpx;
	}

	.noSearchImg {
		width: 310rpx;
		height: 200rpx;
	}

	.noSearchText {
		font-size: 30rpx;
		color: #8F8F8F;
	}
</style>

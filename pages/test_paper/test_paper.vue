<template>
	<view>
		<view v-if="!isDuanWang">
			<!-- 头部 -->
			<view class="test-head flex flex-sb">
				<view class="test-head-tit">
					<image class="test-head-img01" src="../../static/image/search.png"></image>
					<input placeholder="搜索考试名称、老师名称或课程名称" />
					<image class="test-head-img02" src="../../static/image/delete_a.png"></image>
				</view>
				<view class="test-head-btn">取消</view>
			</view>
			<!-- 内容 -->
			<view class="test-paper-con">
				<view class="test-paper-list" v-for="(item,index) in listData" :key='index'>
					<view class="flex test-paper-txt">
						<text class="test-paper-ctxt02">
							<text class="test-paper-ctxt01" v-if="type==1">【模拟考试】</text>
							<text class="test-paper-ctxt01" v-if="type==2">【历年真题】</text>
							<text class="test-paper-ctxt01" v-if="type==3">【考前押题】</text>
							{{item.cont}}
						</text>
					</view>
					<view class="test-paper-time flex">
						<text>{{item.date}}</text>
						<text>{{item.time}}分钟</text>
						<text>{{item.start}}</text>
					</view>
					<view class="zhong flex test-paper-c01">
						<view class="flex" v-if="item.isFree==false">
							<text class="test-paper-ct01">￥</text>
							<text class="test-paper-ct02">{{item.price}}</text>
						</view>
						<text class="test-paper-ct03" v-if="item.isFree==true">免费</text>
						<button class="test-paper-btn" hover-class="none">开始考试</button>
					</view>
				</view>
				<!-- 上拉加载 -->
				<on-more :showLoadMore="isMore" :loadMoreText="loadMoreText"></on-more>
			</view>
		</view>
		<!-- 断网 -->
		<duan-wang :duanWang="isDuanWang"></duan-wang>
	</view>
</template>

<script>
	import duanWang from '@/components/duanWang/duanWang.vue';
	import onMore from '@/components/more/more.vue';
	export default {
		components:{
			duanWang,
			onMore
		},
		data() {
			return {
				/* 上拉加载 */
				isMore: true,
				loadMoreText: '加载中...',
				// 断网：
				isDuanWang: false,
				type:1,//1.模拟考试2.历年真题3.考前押题
				listData:[
					{
						cont:'课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称',
						date:'2020-02-01',
						time:'120',
						start:'未开始',
						price:'23',
						isFree:false
					},{
						cont:'课课程名称课程名称课程名称课程名称课程名称课程名称课程名称程名称',
						date:'2020-02-01',
						time:'120',
						start:'未开始',
						price:'23',
						isFree:true
					},{
						cont:'课程名称',
						date:'2020-02-01',
						time:'120',
						start:'未开始',
						price:'23',
						isFree:false
					}
					
				]
			}
		},
		methods: {
			initData() {
				setTimeout(() => {
					this.max = 0;
					this.listData = [];
					let listData = [];
					this.max += 10;
					for (var i = this.max - 9; i < this.max + 1; i++) {
						listData.push({
						cont:'课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称',
						type:'类型1',
						date:'2020-02-01',
						time:'120',
						start:'未开始',
						price:'23',
						isFree:false
					});
					}
					this.listData = this.listData.concat(listData);
					uni.stopPullDownRefresh();
				}, 300);
			},
			setDate() {
				let listData = [];
				this.max += 10;
				for (var i = this.max - 9; i < this.max + 1; i++) {
					listData.push({
						cont:'课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称',
						type:'类型1',
						date:'2020-02-01',
						time:'120',
						start:'未开始',
						price:'23',
						isFree:false
					});
				}
				this.listData = this.listData.concat(listData);
			}
		},
		onLoad() {
			this.initData();
		},
		onUnload() {
			this.max = 0, this.listData = [], this.loadMoreText = '加载更多', this.showLoadMore = false;
		},
		onReachBottom() {
			console.log('onReachBottom');
			if (this.max > 40) {
				this.loadMoreText = '没有更多数据了!';
				return;
			}
			this.showLoadMore = true;
			setTimeout(() => {
				this.setDate();
			}, 300);
		},
		onPullDownRefresh() {
			console.log('onPullDownRefresh');
			this.initData();
		}
	}
</script>

<style>
page{
	background: #F7F7F7;
}
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
	align-items: center;
}
.test-head-tit{
	width: calc( 100% - 90rpx );
	height: 70rpx;
	background: #f7f7f7;
	border-radius: 40rpx;
	align-items: center;
	display: flex;
	justify-content: space-between;
}
.test-head-tit .test-head-img01{
	margin: 0 20rpx;
	width: 28rpx;
	height: 28rpx;
	display: block;
}
.test-head-img02{
	margin-right: 20rpx;
	width: 28rpx;
	height: 28rpx;
	display: block;
}
.test-head-tit input{
	font-size: 28rpx;
	color: #9A9DA3;
}
.test-head-btn{
	width: 90rpx;
	text-align: center;
	font-size: 28rpx;
	color: #9A9DA3;
}
.test-paper-con{
	margin-top: 180rpx;
	width: 100%;
	height: auto;
	overflow: hidden;
}
.test-paper-list{
	margin-bottom: 30rpx;
	padding: 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	overflow: hidden;
	background: #fff;
}
.test-paper-txt{
	margin-bottom: 20rpx;
	width: 100%;
	max-height: 100rpx;
	overflow: hidden;
	text-overflow: ellipsis;
	display: -webkit-box;
	-webkit-line-clamp: 2;
	-webkit-box-orient: vertical;
}
.test-paper-ctxt01{
	font-size: 30rpx;
	color: #E5252A;
}
.test-paper-ctxt02{
	font-size: 30rpx;
	color: #0C101C;
}
.test-paper-time{
	width: 100%;
}
.test-paper-time text{
	font-size: 26rpx;
	color: #9A9DA3;
	padding-right: 30rpx;
}
.test-paper-c01{
	margin-top: 10rpx;
	justify-content: flex-end;
	width: 100%;
}
.test-paper-ct01{
	font-size: 26rpx;
	color: #E5252A;
}
.test-paper-ct02{
	font-size: 32rpx;
	color: #E5252A;
	font-weight: bold;
}
.test-paper-ct03{
	font-size: 32rpx;
	color: #03b463;
	font-weight: bold;
}
.test-paper-btn{
	margin-left: 30rpx;
	width: 175rpx;
	height: 60rpx;
	line-height: 58rpx;
	text-align: center;
	border: 1px solid #E5252A;
	color: #E5252A;
	font-size: 26rpx;
	border-radius: 50rpx;
	background: #fff !important;
}
</style>

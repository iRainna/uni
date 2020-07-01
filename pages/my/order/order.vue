<template>
	<view>
		<view v-if="!isDuanWang">
			<!-- 头部 -->
			<view class="order-head flex">
				<view class="order-head-img01" @click="goBack"><image src="../../../static/image/nav_Return.png"></image></view>
				<view class="order-head-txt01">我的订单</view>
				<view class="order-head-img02" @click="goClass"><image src="../../../static/image/screen.png"></image></view>
			</view>
			<!-- 内容 -->
			<view v-if="!isNodata" class="order-con">
				<view class="order-tab">
					<text :class="orderType==0?'active':''" @click="selTab(0)">全部</text>
					<text :class="orderType==1?'active':''" @click="selTab(1)">待付款</text>
					<text :class="orderType==2?'active':''" @click="selTab(2)">已付款</text>
					<text :class="orderType==3?'active':''" @click="selTab(3)">已发货</text>
					<text :class="orderType==4?'active':''" @click="selTab(4)">已收货</text>
				</view>
				<view class="order-list">
					<view class="order-list-c01" v-for="(item,index) in listData" :key='index'>
						<view @click="goOrderInfo()">
							<view class="order-cli-tit flex flex-sb">
								<view class="flex">
									<text class="cli-txt01">订单编号:</text>
									<text class="cli-txt02">{{item.number}}</text>
								</view>
								<view class="order-cli-ctxt01" v-if="item.type==1">待付款</view>
								<view class="order-cli-ctxt01" v-if="item.type==2">已付款</view>
								<view class="order-cli-ctxt01" v-if="item.type==3">已发货</view>
								<view class="order-cli-ctxt01" v-if="item.type==4">已收货</view>
							</view>
							<view class="order-list-con">
								<view class="order-cli-con" v-for="(i,index) in item.order" :key='index'>
									<view class="cli-con-txt01">{{i.name}}</view>
									<view class="cli-con-txt02 flex">
										<text>数量：{{i.num}}</text>
										<text>单价：￥{{i.price}}</text>
									</view>
								</view>
							</view>
							<view class="cli-con-txt03 flex">
								<text class="cli-cnum">共{{item.allNum}}件商品,总计:</text>
								<text class="cli-cprice">￥{{item.sum}}</text>
							</view>
						</view>
						<view class="order-btn">
							<!-- /*1，待付款 2、已付款 3.已发货 4.已收货 */ -->
							<button class="order-con-btn01" hover-class="none" v-if="item.type==1" @click="cancelBtn">取消订单</button>
							<button class="order-con-btn02" hover-class="none" v-if="item.type==1" @click="goOrderInfo()">去付款</button>
							<button class="order-con-btn02" hover-class="none" v-if="item.type==3" @click="goOrderInfo()">确认收货</button>
							<button class="order-con-btn01" hover-class="none" v-if="item.type==4" @click="dancelBtn">删除订单</button>
							<button class="order-con-btn02" hover-class="none" v-if="item.type==4" @click="goPj">评论</button>
						</view>
					</view>
					<!-- 上拉加载 -->
					<on-more :showLoadMore="isMore" :loadMoreText="loadMoreText"></on-more>
				</view>
			</view>
			<!-- 暂无数据 -->
			<no-data :isNoText="isNoText" :nodata="isNodata" v-else></no-data>
		</view>
		<!-- 取消订单弹窗 start-->
		<view class="popup" v-show="isCancel" @touchmove.stop.prevent="moveHandle">
			<view class="order-popup animated fadeIn">
				<view class='order-cancel-tit'>提示</view>
				<view class="order-cancel-txt">
					您确定要取消该订单吗？
				</view>
				<view class="order-cancel-btn">
					<button class="cancel-pop-btn01" @click="cancelBtn">取消</button>
					<button class="cancel-pop-btn02">确认</button>
				</view>
			</view>
		</view>
		<!-- 取消订单弹窗 end>
		<!-- 删除订单弹窗 start-->
		<view class="popup" v-show="isDelete" @touchmove.stop.prevent="moveHandle">
			<view class="order-popup animated fadeIn">
				<view class='order-cancel-tit'>提示</view>
				<view class="order-cancel-txt">
					您确定要删除该订单吗？
				</view>
				<view class="order-cancel-btn">
					<button class="cancel-pop-btn01" @click="dancelBtn">取消</button>
					<button class="cancel-pop-btn02">确认</button>
				</view>
			</view>
		</view>
		<!-- 删除订单弹窗 end>
		<!-- 断网 -->
		<duan-wang :duanWang="isDuanWang"></duan-wang>
	</view>
</template>

<script>
	import duanWang from '@/components/duanWang/duanWang.vue';
	import noData from '@/components/noData/noData.vue';
	import onMore from '@/components/more/more.vue';
	export default {
		components:{
			duanWang,
			noData,
			onMore
		},
		data() {
			return {
				/* 删除订单 */
				isDelete:false,
				/* 取消订单 */
				isCancel:false,
				/* 0.全部 1，待付款 2、已付款 3.已发货 4.已收货 */
				orderType:0,
				// 断网：
				isDuanWang: false,
				/* 判断是否有数据 */
				isNodata:false,
				isNoText: '-你还没有订单哦-',
				/* 上拉加载 */
				isMore: true,
				loadMoreText: '加载中...',
				listData:[
					{
						number:'000000000002',
						type:1,//1，待付款 2、已付款 3.已发货 4.已收货
						order:[
							{
								name:'课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称',
								num:'1',
								price:'40',
							},
							{
								name:'课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称',
								num:'1',
								price:'40',
							}
						],
						allNum:'7',
						sum:'990'
					},
					{
						number:'000000000002',
						type:2,//1，待付款 2、已付款 3.已发货 4.已收货
						order:[
							{
								name:'课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称',
								num:'1',
								price:'40',
							}
						],
						allNum:'7',
						sum:'990'
					},
					{
						number:'000000000002',
						type:3,//1，待付款 2、已付款 3.已发货 4.已收货
						order:[
							{
								name:'课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称',
								num:'1',
								price:'40',
							}
						],
						allNum:'7',
						sum:'990'
					},
					{
						number:'000000000002',
						type:4,//1，待付款 2、已付款 3.已发货 4.已收货
						order:[
							{
								name:'课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称',
								num:'1',
								price:'40',
							}
						],
						allNum:'7',
						sum:'990'
					}
				],
			}
		},
		methods: {
			/* 分类 */
			goClass(){
				uni.navigateTo({
					url:'/pages/index/intention/intention'
				})
			},
			/* 去评价 */
			goPj(){
				uni.navigateTo({
					url:'/pages/my/order_pj/order_pj'
				})
			},
			/* 删除订单弹窗 */
			dancelBtn(){
				this.isDelete = !this.isDelete
			},
			/* 取消订单弹窗 */
			cancelBtn(){
				this.isCancel = !this.isCancel
			},
			moveHandle(){},
			/* 订单详情 */
			goOrderInfo(){
				uni.navigateTo({
					url:'/pages/my/order_info/order_info'
				})
			},
			/* 切换 */
			selTab(id){
				this.orderType = id
			},
			/* 返回上级页面 */
			goBack() {
				uni.navigateBack({
					delta:1
				})
			},
			initData() {
				setTimeout(() => {
					this.max = 0;
					this.listData = [];
					let listData = [];
					this.max += 10;
					for (var i = this.max - 9; i < this.max + 1; i++) {
						listData.push({
						number:'000000000002',
						type:4,//1，待付款 2、已付款 3.已发货 4.已收货
						order:[
							{
								name:'课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称',
								num:'1',
								price:'40',
							},
							{
								name:'课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称',
								num:'1',
								price:'40',
							}
						],
						allNum:'7',
						sum:'990'
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
						number:'000000000002',
						type:1,//1，待付款 2、已付款 3.已发货 4.已收货
						order:[
							{
								name:'课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称',
								num:'1',
								price:'40',
							},
							{
								name:'课程名称课程名称课程名称课程名称课程名称课程名称课程名称课程名称',
								num:'1',
								price:'40',
							}
						],
						allNum:'7',
						sum:'990'
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
.order-head{
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
.order-head-img01{
	margin-left: 30rpx;
	width: 44rpx;
	height: 44rpx;
}
.order-head-img01 > image{
	width: 100%;
	height: 100%;
	display: block;
}
.order-head-txt01{
	flex: 1;
	text-align: center;
	font-size: 32rpx;
	color: #000000;
}
.order-head-img02{
	margin-right: 30rpx;
	width: 44rpx;
	height: 44rpx;
}
.order-head-img02 > image{
	width: 100%;
	height: 100%;
	display: block;
}
.order-con{
	margin-top: 132rpx;
	width: 100%;
	height: auto;
	overflow: hidden;
}
.order-tab{
	padding: 30rpx 0;
	display: flex;
	width: 100%;
	height: auto;
	background: #fff;
	position: fixed;
	z-index: 9;
}
.order-tab text {
	width: 20%;
	text-align: center;
	font-size: 30rpx;
	display: block;
	position: relative;
	color: #9a9da3;
}

.order-tab text::after {
	content: '';
	width: 18rpx;
	height: 6rpx;
	background-color: #fff;
	position: absolute;
	left: 50%;
	bottom: -12rpx;
	margin-left: -9rpx;
	z-index: 0;
	border-radius: 20rpx;
}

.order-tab .active {
	color: #0C101C;
	font-weight: bold;
}

.order-tab .active::after {
	background-color: #0C101C;
}
.order-list{
	margin-top: 90rpx;
	width: 100%;
	height: auto;
}
.order-list-c01{
	margin-bottom: 30rpx;
	padding: 40rpx 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	background: #fff;
}
.order-cli-tit{
	width: 100%;
}
.cli-txt01{
	font-size: 28rpx;
	color: #0C101C;
}
.cli-txt02{
	font-size: 28rpx;
	color: #9A9DA3;
}
.order-cli-ctxt01{
	font-size: 28rpx;
	color: #E5252A;
}
.order-list-con{
	width: 100%;
	height: auto;
}
.order-cli-con{
	padding-bottom: 30rpx;
	width: 100%;
	height: auto;
	background: #fff;
	border-bottom: 1rpx solid #eee;
}
.order-cli-con:last-child{
	border-bottom: 0px;
}
.cli-con-txt01{
	padding: 30rpx 0;
	width: 100%;
	font-size: 28rpx;
	color: #0C101C;
}
.cli-con-txt02{
	width: 100%;
	align-items: center;
}
.cli-con-txt02 text{
	font-size: 24rpx;
	color: #9A9DA3;
	padding-right: 30rpx;
}
.cli-con-txt03{
	width: 100%;
	justify-content: flex-end;
	align-items: center;
}
.cli-cnum{
	font-size: 28rpx;
	color: #0C101C;
}
.cli-cprice{
	font-size: 32rpx;
	color: #E5252A;
	font-weight: bold;
}
.order-btn{
	margin-top: 40rpx;
	width: 100%;
	display: flex;
	justify-content: flex-end;
	align-items: center;
}
.order-btn button{
	width: 175rpx;
	height: 60rpx;
	background: #fff !important;
	text-align: center;
	line-height: 58rpx;
	font-size: 26rpx;
	margin-left: 30rpx;
	border-radius: 40rpx;
}
.order-btn .order-con-btn01{
	border: 1rpx solid #cecece;
	color: #0C101C;
}
.order-btn .order-con-btn02{
	border: 1rpx solid #E5252A;
	color: #E5252A;
}

</style>

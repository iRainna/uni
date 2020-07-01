<template>
	<view>
		<view v-if="!isDuanWang">
			<view v-if="isNodata" class="address-content">
				<view class="address-con01" v-for="(item,index) in list" :key='index'>
					<view class="address-con-li">
						<view class="flex">
							<text class="address-ctxt01">{{item.name}}</text>
							<text class="address-ctxt02">{{item.phone}}</text>
						</view>
						<view class="address-con-txt">{{item.address}}</view>
					</view>
					<view class="flex flex-sb">
						<view class="flex zhong address-con-deft" @click="defBtn(index)">
							<view class="address-con-img01">
								<image :src="isDefaule==index?'../../../static/image/Single_a.png':'../../../static/image/Single_aa.png'"></image>
							</view>
							<text :class="isDefaule==index?'address-con-txt01':'address-con-txt02'">默认地址</text>
						</view>
						<view class="flex">
							<view class="flex zhong">
								<view class="address-con-img02"><image src="../../../static/image/Myaddress_edit.png"></image></view>
								<text class="address-ctxt03">编辑</text>
							</view>
							<view class="flex zhong mag-left5">
								<view class="address-con-img02"><image src="../../../static/image/del_icon01.png"></image></view>
								<text class="address-ctxt03">删除</text>
							</view>
						</view>
					</view>
				</view>
			</view>
			<!-- 暂无数据 -->
			<view class="noAddress" v-else>
				<image src="../../../static/image/bg_b.png" mode=""></image>
				<text>-还没有地址，快去新增吧-</text>
			</view>
			<view class="address-btn"><button hover-class="none" @click="goAdd">新增收货地址</button></view>
		</view>
		<!-- 断网 -->
		<duan-wang :duanWang="isDuanWang"></duan-wang>
	</view>
</template>

<script>
	import duanWang from '@/components/duanWang/duanWang.vue'
	export default {
		components:{
			duanWang
		},
		data() {
			return {
				// 断网：
				isDuanWang: false,
				/* 判断是否有数据 */
				isNodata:true,
				list:[
					{
						name:'小明',
						phone:'12111111111',
						address:'四川省遂宁市白鹤镇14村5社',
						id:1
					},
					{
						name:'小明',
						phone:'12111111111',
						address:'四川省遂宁市白鹤镇14村5社',
						id:2
					}
				],
				isDefaule:''
			}
		},
		methods: {
			defBtn(index){
				this.isDefaule = index
			},
			/* 添加地址 */
			goAdd(){
				uni.navigateTo({
					url:'/pages/my/address_add/address_add'
				})
			}
		}
	}
</script>

<style>
page{
	background: #F7F7F7;
}
.mag-left5{
	margin-left: 50rpx;
}
.noAddress{
	width: 100%;
	height: auto;
	overflow: hidden;
	margin-top: 30%;
}
.noAddress image{
	margin: 0 auto;
	width: 310rpx;
	height: 200rpx;
	display: block;
}
.noAddress text{
	font-size: 28rpx;
	color: #666;
	display: block;
	text-align: center;
}
.address-btn{
	padding:20rpx 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	background: #fff;
	position: fixed;
	bottom: 0;
	left: 0;
	box-shadow: 0 0 15px #ccc;
}
.address-btn button{
	width: 100%;
	height: 90rpx;
	line-height: 90rpx;
	text-align: center;
	border-radius: 10rpx;
	background-image: linear-gradient(to right,#e83035, #fa7276)  !important;
	font-size: 28rpx;
	color: #fff;
}
.address-content{
	width: 100%;
	height: auto;
	overflow: hidden;
	border-top: 1px solid #eee;
}
.address-con01{
	margin-bottom: 30rpx;
	width: calc( 100% - 60rpx );
	padding: 40rpx 30rpx 30rpx 30rpx;
	height: auto;
	background: #fff;
}
.address-con-li{
	margin-bottom: 30rpx;
	width: 100%;
	height: auto;
	overflow: hidden;
	border-bottom: 1rpx solid #eee;
}
.address-ctxt01{
	font-size: 30rpx;
	color: #0C101C;
}
.address-ctxt02{
	margin-left: 25rpx;
	padding-left: 20rpx;
	position: relative;
	font-size: 28rpx;
	color: #9A9DA3;
}
.address-ctxt02::after{
	content: '';
	position: absolute;
	width: 1rpx;
	height: 30rpx;
	background: #eee;
	left: 0;
	top:0;
	margin-top:4rpx;
}
.address-con-txt{
	padding: 30rpx 0;
	width: 100%;
	font-size: 28rpx;
	color: #0C101C;
}
.address-con-txt01{
	font-size: 28rpx;
	color: #0C101C;
}
.address-con-txt02{
	font-size: 28rpx;
	color: #9A9DA3;
}
.address-con-img01{
	width: 40rpx;
	height: 40rpx;
	margin-right: 20rpx;
}
.address-con-img01 image{
	width: 100%;
	height: 100%;
	display: block;
}
.address-con-img02{
	width: 24rpx;
	height: 24rpx;
}
.address-con-img02 image{
	width: 100%;
	height: 100%;
	display: block;
}
.address-ctxt03{
	padding-left: 20rpx;
	font-size: 28rpx;
	color: #9A9DA3;
}

</style>

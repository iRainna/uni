<template>
	<view>
		<view v-if="!isDuanWang">
			<view class="address-add-content">
				<view class="address-add-c01">
					<view class="address-add-txt01">收货人</view>
					<input class="address-add-input01" placeholder="请输入收货人姓名" />
				</view>
				<view class="address-add-c01">
					<view class="address-add-txt01">联系电话</view>
					<input class="address-add-input01" placeholder="请输入联系电话" />
				</view>
				<view class="address-add-c01">
					<view class="address-add-txt01">选择城市</view>
					<view class="add-city">
						<pick-regions :defaultRegions="defaultRegions" @getRegions="handleGetRegions" :class="isCity ? 'hair_ding' : ''">
							<text class="input_color hui">选择所在区域</text>
						</pick-regions>
						<text>{{ regionsName }}</text>
						<image src="../../../static/image/choose.png" mode=""></image>
					</view>
				</view>
				<view class="address-add-c01">
					<view class="address-add-txt01">详细地址</view>
					<input class="address-add-input01" placeholder="请输入详细地址" />
				</view>
			</view>
			<view class="address-btn"><button hover-class="none">保存</button></view>
		</view>
		<!-- 断网 -->
		<duan-wang :duanWang="isDuanWang"></duan-wang>
	</view>
</template>

<script>
	import duanWang from '@/components/duanWang/duanWang.vue'
	// 省市区
	import pickRegions from '@/components/pick-regions/pick-regions.vue';
	export default {
		components:{
			duanWang,
			pickRegions
		},
		data() {
			return {
				// 断网：
				isDuanWang: false,
				// 省市区
				isCity: false,
				regions: [],
				defaultRegions: ['广东省', '广州市', '番禺区'],
			}
		},
		methods: {
			// 获取选择的地区
			handleGetRegions(regions) {
				this.regions = regions;
				this.isCity = true;
			},
		},
		computed: {
			regionsName() {
				// 转为字符串
				
				var City=this.regions.map(item => item.name).join(' - ');
				this.City=City;
				console.log(this.City);
				return City;
			}
		},
		
	}
</script>

<style>
page{
	background: #F7F7F7;
}
.hair_ding {
	position: absolute;
	width: 100%;
	height: 100%;
	opacity: 0;
	left: 0;
	top: 0;
	z-index: 20;
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
.address-add-content{
	padding: 0 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	overflow: hidden;
	background: #fff;
	border-top: 1px solid #eee;
}
.address-add-c01{
	padding: 30rpx 0;
	height: auto;
	width: 100%;
	border-bottom: 1px solid #eee;
}
.address-add-txt01{
	width: 100%;
	font-size: 28rpx;
	color: #0C101C;
	padding-bottom: 30rpx;
}
.address-add-input01{
	width: 100%;
	font-size: 26rpx;
	color: #9A9DA3;
}
.add-city{
	width: 100%;
	display: flex;
	justify-content: space-between;
	align-items: center;
	position: relative;
}
.add-city text{
	font-size: 28rpx;
	color: #9A9DA3;
}
.add-city image{
	width: 11rpx;
	height: 24rpx;
	display: block;
}
</style>

<template>
	<view>
		<view v-if="!isDuanWang">
			<view class="help-content">
				<view class="help-con" v-for="(item,index) in list" :key='index' @click="goHelpInfo">
					<text>{{item.name}}</text>
					<image src="../../../static/image/choose.png"></image>
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
						name:'帮助中心帮助中心帮助中心帮助中心帮助中心帮助中心'
					},
					{
						name:'帮助中心帮助中心帮助中心帮助中心帮助中心帮助中心'
					},{
						name:'帮助中心帮助中心帮助中心帮助中心帮助中心帮助中心'
					},{
						name:'帮助中心帮助中心帮助中心帮助中心帮助中心帮助中心'
					},{
						name:'帮助中心帮助中心帮助中心帮助中心帮助中心帮助中心'
					},{
						name:'帮助中心帮助中心帮助中心帮助中心帮助中心帮助中心'
					},{
						name:'帮助中心帮助中心帮助中心帮助中心帮助中心帮助中心'
					}
				]
			}
		},
		methods: {
			/* 详情 */
			goHelpInfo(){
				uni.navigateTo({
					url:'/pages/my/help_info/help_info'
				})
			}
		}
	}
</script>

<style>
page{
	background: #F7F7F7;
}
.help-content{
	padding: 0 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	overflow: hidden;
	border-top: 1px solid #eee;
	background: #fff;
}
.help-con{
	padding: 25rpx 0;
	width: 100%;
	display: flex;
	justify-content: space-between;
	align-items: center;
	border-bottom: 1rpx solid #eee;
}
.help-con:last-child{
	border-bottom: 0rpx;
}
.help-con text{
	width: calc( 100% - 30rpx );
	height: 50rpx;
	line-height: 50rpx;
	font-size: 28rpx;
	color: #0C101C;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
}
.help-con image{
	width: 11rpx;
	height: 24rpx;
	display: block;
}

</style>

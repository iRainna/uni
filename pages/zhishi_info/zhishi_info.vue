<template>
	<view>
		<view v-if="!isDuanWang">
			<view class="zhishiInfo-cont">
				<view class="zhishi-info-tit">课程名称</view>
				<view class="zhishi-info-ctxt">
					知识点知识点知识点知识点知识点知识点知识点知识点知识点
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
				isDuanWang: false
			}
		},
		methods: {
			
		}
	}
</script>

<style>
.zhishiInfo-cont{
	padding: 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	overflow: hidden;
	border-top: 1px solid #eee;
}
.zhishi-info-tit{
	padding: 30rpx 0;
	width: 100%;
	height: auto;
	font-size: 40rpx;
	color: #0C101C;
	font-weight: bold;
}
.zhishi-info-ctxt{
	width: 100%;
	height: auto;
	overflow: hidden;
	font-size: 28rpx;
	color: #0C101C;
	line-height: 44rpx;
}
</style>

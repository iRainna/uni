<template>
	<view>
		<view v-if="!isDuanWang">
			<view class="tika-conter flex flex-fw">
				<view class="tika-con" v-for="(item,index) in list" :key='index'>
					<text :class="item.isError?'error':''">{{item.num}}</text>
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
					{num:'1',isError:true},
					{num:'2',isError:true},
					{num:'3',isError:false},
					{num:'4',isError:false},
					{num:'5',isError:false},
					{num:'6',isError:false},
					{num:'7',isError:false}
				]
			}
		},
		methods: {
			
		}
	}
</script>

<style>
.tika-conter{
	padding: 30rpx 0;
	width: 100%;
	height: auto;
	overflow: inherit;
	border-top: 30rpx solid #f7f7f7;
}
.tika-con{
	width: calc( 100% / 6 );
}
.tika-con text{
	margin: 30rpx auto;
	width: 90rpx;
	height: 90rpx;
	background: #fff;
	border: 1px solid #9a9da3;
	text-align: center;
	line-height: 90rpx;
	font-size: 36rpx;
	color: #9A9DA3;
	border-radius: 50%;
	font-weight: bold;
	display: block;
}
.tika-con .error{
	background: #fbe3ec;
	color: #ec74a1;
	border: 1px solid #fbe3ec;
}
</style>

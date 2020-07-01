<template>
	<view>
		<view v-if="!isDuanWang">
			<view class="section-content" v-for="(item,index) in list" :key='index'>
				<view class="section-cont01 flex flex-sb">
					<view class="flex section-con-cli01" @click="up(item)">
						<view class="section-con-img">
							<image :src="item.hide?'../../static/image/chapter_c.png':'../../static/image/chapter_a.png'"></image>
						</view>
						<text class="section-con-txt01">{{item.section}}</text>
						<text class="section-con-txt02">{{item.sectionName}}</text>
					</view>
					<view class="flex">
						<text class="section-con-ctxt01">知识点:{{item.page}}</text>
					</view>
				</view>
				<view class="section-cont02" v-show="item.hide">
					<view class="section-cli01 flex" v-for="(t,id) in item.sectionClass" :key='id'>
						<view class="flex section-con-cli01" @click="goInfo">
							<view class="section-con-img02">
								<image src="../../static/image/chapter_b.png"></image>
							</view>
							<text class="section-cli-txt01">{{t.name}}</text>
							<text class="section-cli-txt02">{{t.con}}</text>
						</view>
					</view>
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
						section:'第一章',
						sectionName:'章节名称',
						page:'10',
						sectionClass:[
							{
								name:'第一节',
								con:'章节名称',
								page:'20'
							},
							{
								name:'第一节',
								con:'章节名称',
								page:'20'
							}
						],
						hide:false,
					},{
						section:'第一章',
						sectionName:'章节名称',
						page:'50',
						sectionClass:[
							{
								name:'第一节',
								con:'章节名称',
								page:'20'
							},
							{
								name:'第一节',
								con:'章节名称',
								page:'50'
							},{
								name:'第一节',
								con:'章节名称',
								page:'50'
							}
						],
						hide:false,
					},{
						section:'第一章',
						sectionName:'章节名称',
						page:'10',
						sectionClass:[
							{
								name:'第一节',
								con:'章节名称',
								page:'50'
							},
							{
								name:'第一节',
								con:'章节名称',
								page:'50'
							},{
								name:'第一节',
								con:'章节名称',
								page:'50'
							}
						],
						hide:false,
					}
				],
				upId:'',
				
			}
		},
		methods: {
			/* 收起展开 */
			up(index){
				this.upId = index;
				index.hide = !index.hide;
			},
			/* 知识点详情 */
			goInfo(){
				uni.navigateTo({
					url:'/pages/zhishi_info/zhishi_info'
				})
			}
		}
	}
</script>

<style>
.section-content{
	border-top: 1px solid #eee;
	width: 100%;
	height: auto;
	overflow: hidden;
}
.section-cont01{
	padding:30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	overflow: hidden;
	align-items: center;
}
.section-con-cli01{
	width: calc( 100% - 200rpx );
	align-items: center;
}
.section-con-img{
	width: 35rpx;
	height: 35rpx;
}
.section-con-img image{
	width: 100%;
	height: 100%;
	display: block;
}
.section-con-txt01{
	padding-left: 20rpx;
	font-size: 32rpx;
	color: #0C101C;
	font-weight: bold;
}
.section-con-txt02{
	width: calc( 100% - 200rpx );
	height: 44rpx;
	overflow: hidden;
	padding-left: 30rpx;
	font-size: 32rpx;
	color: #0C101C;
	font-weight: bold;
	text-overflow: ellipsis;
	white-space: nowrap;
}
.section-con-ctxt01{
	font-size: 26rpx;
	color: #0C101C;
}
.section-con-ctxt02{
	padding-left: 20rpx;
	font-size: 26rpx;
	color: #9A9DA3;
}
.section-cont02{
	padding: 0 30rpx;
	width: calc( 100% - 60rpx );
	height: auto;
	background: #F7F7F7;
	position: relative;
}
.section-cont02::after{
	width:3px;
	height: 10000rpx;
	border-left: 1px solid #E5252A;
	position: absolute;
	content: '';
	left: 44rpx;
	top: 0;
	margin-top: -44rpx;
}
.section-cli01{
	width: 100%;
	height: auto;
	padding: 30rpx 0;
}
.section-cli-txt01{
	padding-left: 20rpx;
	font-size: 30rpx;
	color: #0C101C;
}
.section-cli-txt02{
	width: calc( 100% - 180rpx );
	height: 44rpx;
	overflow: hidden;
	padding-left: 30rpx;
	font-size: 30rpx;
	color: #0C101C;
	text-overflow: ellipsis;
	white-space: nowrap;
}
.section-con-img02{
	margin-left: 8rpx;
	width: 18rpx;
	height: 18rpx;
}
.section-con-img02 image{
	width: 100%;
	height: 100%;
	display: block;
}
.heid{
	display: none;
}
</style>

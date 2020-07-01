<template>
	<view class="login">
		<view class="title">账号密码登录</view>
		<view class="login_div">
			<form action="">
				<view class="login_li zhong float">
					<image src="../../../static/image/regsiter-a.png" mode=""></image>
					<view class="login_input">
						<input type="text" value="" placeholder="请输入手机号码" v-model="call" @input='telInput' placeholder-style="color:#999999;"/>
					</view>
				</view>
				<view class="login_li zhong float">
					<image src="../../../static/image/regsiter-c.png" mode=""></image>
					<view class="login_input">
						<input type="text" value="" placeholder="请输入密码" v-model="pass" @input='telInput' placeholder-style="color:#999999;"/>
					</view>
				</view>
				<view class="login_hg float zhong">
					<text @click="regClick()">马上注册</text>
					<text @click="passClick()">忘记密码?</text>
				</view>
				<button type="default" hover-class="none" class="login_btn" :class="isLogin?'hui':''" @click="intention()">登录</button>
			</form>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				isLogin:true,
				call:'',
				pass:''
			}
		},
		methods: {
			
			telInput(){
				var that=this;
				setTimeout(function(){
					if(that.call.length > 0 && that.pass.length  > 0 ){
						that.isLogin = false
					}else{
						that.isLogin = true
					}
				},20)
			},
			
			// 注册
			regClick(){
				uni.navigateTo({
					url:'/pages/index/regsit/regsit'
				})
			},
			// 忘记密码
			passClick(){
				uni.navigateTo({
					url:'/pages/index/passWord/passWord'
				})
			},
			// 选意向
			intention(){
				uni.navigateTo({
					url:'/pages/index/intention/intention'
				})
			},
			
		}
	}
</script>

<style>

.login_btn.hui{
  background: #b3b3b3 !important;
}

.login_btn{
	overflow: hidden;
	height: 88rpx;
	display: block;
	 background: linear-gradient(to right, #e93237 , #fa7276) !important; /* 标准的语法 */
    color: #fff !important;
	text-align: center;
	line-height: 88rpx;
	font-size: 28rpx;
}	

.login_hg text{
	font-size: 28rpx;
	color: #333;
}	

.login_hg{
	overflow: hidden;
	display: flex;
	margin-top: 28rpx;
	margin-bottom: 60rpx;
}	

.login_input input{
	overflow: hidden;
	width: 100%;
	font-size: 28rpx;
	color:#333 ;
}	

.login_input{
	width: calc( 100% - 57rpx );
	overflow: hidden;
}
	
.login_li image{
	display: block;
	width:40rpx;
	height: 40rpx;
}	

.login_li{
	overflow: hidden;
	display: flex;
	padding-bottom: 30rpx;
	border-bottom: solid 1px #cccccc;
	margin-top: 64rpx;
}	

.login_div{
	overflow: hidden;
	margin-top: 50rpx;
}	

.title{
	overflow: hidden;
	font-size: 44rpx;
	color: #333;
	padding-top: 172rpx;
	font-weight: 600;
}	

.login{
	padding-left: 60rpx;
	padding-right: 60rpx;
	overflow: hidden;
}	
	
page{
	width: 100%;
	height: 100%;
	overflow: hidden;
}
</style>

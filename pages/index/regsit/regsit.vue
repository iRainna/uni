<template>
	<view class="login">
		<view class="title">新用户注册</view>
		<view class="login_div">
			<form action="">
				<view class="login_li zhong float">
					<image src="../../../static/image/regsiter-a.png" mode=""></image>
					<view class="login_input">
						<input type="text" value="" placeholder="请输入注册手机号码" v-model="call" @input='telInput' placeholder-style="color:#999999;"/>
					</view>
				</view>
				<view class="login_li zhong float">
					<image src="../../../static/image/regsiter-b.png" mode=""></image>
					<view class="login_input">
						<input type="text" value="" placeholder="请输入短信验证码" v-model="yan" @input='telInput' placeholder-style="color:#999999;"/>
					 <button @click="getCode(formData)" class="code-btn" hover-class="none" :disabled="!show">
					         <text v-show="show">获取验证码</text>
					         <text v-show="!show" class="count">重新获取{{count}}s</text>
					     </button>
					</view>
				</view>
				<view class="login_li zhong float">
					<image src="../../../static/image/regsiter-c.png" mode=""></image>
					<view class="login_input">
						<input type="text" value="" placeholder="请设置6-20位登录密码" v-model="pass" @input='telInput' placeholder-style="color:#999999;"/>
					</view>
				</view>
				<view class="login_li zhong float">
					<image src="../../../static/image/regsiter-c.png" mode=""></image>
					<view class="login_input">
						<input type="text" value="" placeholder="请再次确认登录密码" v-model="passb" @input='telInput' placeholder-style="color:#999999;"/>
					</view>
				</view>
				
				<view class="reg_fg zhong">
					<image src="../../../static/image/regBtn.png" mode=""></image>
					<view class="reg_text zhong">同意<text @click="xieClick()">《用户服务协议》</text></view>
				</view>
				
				<button type="default" hover-class="none" class="login_btn" :class="isRegsit?'hui':''" >注册</button>
				<view class="reg_login" @click="loginClick()">已有账户，立即登录</view>
			</form>
		</view>
	</view>
</template>

<script>
	const TIME_COUNT = 60;
	export default {
		
		data() {
			return {
				isRegsit:true,
				call:'',
				yan:'',
				pass:'',
				passb:'',
				// 倒计时
				 show: true,
				        count: '',
				        timer: null,
			}
		},
		methods: {
			
			telInput(){
				var that=this;
				setTimeout(function(){
					if(that.call.length > 0 && that.pass.length  > 0 && that.yan.length > 0 && that.passb.length  > 0 ){
						that.isRegsit = false
					}else{
						that.isRegsit = true
					}
				},20)
			},
			// 倒计时
			 getCode(formData){
			            if (!this.timer) {
			                this.count = TIME_COUNT;
			                this.show = false;
			                this.timer = setInterval(() => {
			                  if (this.count > 0 && this.count <= TIME_COUNT) {
			                    this.count--;
			                  } else {
			                    this.show = true;
			                    clearInterval(this.timer);
			                    this.timer = null;
			                  }
			                }, 1000)
			              }
			
			},
			// 注册
			xieClick(){
				uni.navigateTo({
					url:'/pages/index/agree/agree'
				})
			},
			// 登录
			loginClick(){
				uni.redirectTo({
					url:'/pages/index/login/login'
				})
			},
			
		}
	}
</script>

<style>

.reg_login{
	font-size: 26rpx;
	color: #333;
	text-align: center;
	margin-top: 42rpx;
}

/* reg_login */	

.reg_text text{
	color: #078fee;
}

.reg_text{
	overflow: hidden;
	font-size: 26rpx;
	color: #999999;
}

.reg_fg image{
	display: block;
	width: 22rpx;
	height: 22rpx;
	margin-right: 0.5em;
}	

.reg_fg{
	overflow: hidden;
	display: flex;
	margin-top: 60rpx;
	margin-bottom: 60rpx;
}

/* reg_fg */	

.login_input button{
	width: 175rpx;
	height: 50rpx;
	background-color: #f65857 !important;
	font-size: 28rpx;
	color: #fff !important;
	text-align: center;
	line-height: 50rpx;
	position: absolute;
	right: 0;
	top: 50%;
	margin-top: -25rpx;
	border-radius: 6rpx;
}

/* login_input */	

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
	position: relative;
}
	
.login_li image{
	display: block;
	width:40rpx;
	height: 40rpx;
}	

.login_li{
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
	padding-top:90rpx;
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

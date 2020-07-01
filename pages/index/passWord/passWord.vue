<template>
	<view class="pass">
		<view class="pass_head">
			<view class="pass_text  active">
				<text>1</text>
				<text>验证手机</text>
			</view>
			<view class="pass_text" :class="!isForm ? 'active' : ''">
				<text>2</text>
				<text>设置新密码</text>
			</view>
		</view>

		<!-- 验证手机 -->
		<view class="pass_yan" v-if="isForm">
			<view class="login_li zhong ">
				<image src="../../../static/image/regsiter-a.png" mode=""></image>
				<view class="login_input"><input type="text" placeholder="请输入注册手机号码" v-model="call" @input="telInput" placeholder-style="color:#999;" /></view>
			</view>
			<view class="login_li zhong ">
				<image src="../../../static/image/regsiter-b.png" mode=""></image>
				<view class="login_input"><input type="number" placeholder="请输入短信验证码" v-model="yan" @input="telInput" placeholder-style="color:#999;" /></view>
				<button hover-class="none" @click="getCode(formData)" class="login_see" :disabled="!show">
					<text v-show="show">获取验证码</text>
					<text v-show="!show" class="count">重新发送{{ count }}s</text>
				</button>
			</view>
			<view class="login_btn" :class="isDown ? '' : 'opacity'"><button hover-class="none" @click="downClick()">下一步</button></view>
		</view>
		<!-- 设置新密码 -->
		<view class="pass_yan" v-else>
			<view class="login_li zhong ">
				<image src="../../../static/image/regsiter-c.png" mode=""></image>
				<view class="login_input"><input type="text" placeholder="请设置6-20位登录密码" password="true" maxlength="20" placeholder-style="color:#999;" /></view>
			</view>
			<view class="login_li zhong ">
				<image src="../../../static/image/regsiter-c.png" mode=""></image>
				<view class="login_input"><input type="text" placeholder="请再次确认登录密码" password="true" maxlength="20" placeholder-style="color:#999;" /></view>
			</view>
			<view class="login_btn" :class="isDown ? '' : 'opacity'"><button hover-class="none" @click="login()">提交</button></view>
		</view>
	</view>
</template>

<script>
const TIME_COUNT = 60;
export default {
	data() {
		return {
			// 倒计时
			show: true,
			count: '',
			timer: null,
			// 判断
			isForm: true,
			// 验证
			call: '',
			yan: '',
			// 验证对了按钮变色
			isDown: false
		};
	},
	methods: {
		// 验证
		telInput() {
			var that = this;
			setTimeout(function() {
				if (that.call.length > 0 && that.yan.length > 0) {
					that.isDown = true;
				} else {
					that.isDown = false;
				}
			}, 20);
		},
		downClick() {
			this.isForm = false;
		},
		// 倒计时
		getCode(formData) {
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
				}, 1000);
			}
		},
		login(){
			uni.redirectTo({
				url:'/pages/index/login/login'
			})
		}
	}
};
</script>

<style>
.login_btn {
	overflow: hidden;
}

.login_btn button {
	overflow: hidden;
	height: 100rpx;
	background-color: #b3b3b3 !important;
	font-size: 28rpx;
	color: #fff !important;
	text-align: center;
	line-height: 100rpx;
	margin-top: 90rpx;
}

.login_see {
	width: 175rpx;
	height: 50rpx;
	background-color: #f65857 !important;
	font-size: 28rpx;
	color: #fff !important;
	text-align: center;
	line-height: 50rpx;
	position: absolute;
	right: 0;
	top: 62%;
	margin-top: -25rpx;
	border-radius: 6rpx;
}

.login_input input {
	overflow: hidden;
	width: 100%;
	height: 100%;
	font-size: 28rpx;
	color: #333;
}

.login_input {
	overflow: hidden;
	width: calc(100% - 72rpx);
}

.login_li > image {
	display: block;
	width: 40rpx;
	height: 40rpx;
	margin-right: 20rpx;
}

.login_li {
	overflow: hidden;
	padding-bottom: 30rpx;
	padding-top: 65rpx;
	border-bottom: solid 1px #f5f5f5;
	display: flex;
	position: relative;
}

.register_form {
	overflow: hidden;
	margin-top: 40rpx;
}
.pass_yan {
	overflow: hidden;
	padding-left: 60rpx;
	padding-right: 60rpx;
}

/* pass_yan */

.active text:first-child {
	color: #fff !important;
	background-color: #333 !important;
}

.active text {
	color: #333 !important;
}

.pass_text text:first-child {
	width: 60rpx;
	height: 60rpx;
	border-radius: 50%;
	display: block;
	background-color: #e4e4e4;
	font-size: 28rpx;
	color: #8f8f8f;
	text-align: center;
	line-height: 60rpx;
	margin: 0 auto 20rpx auto;
}

.pass_text text {
	font-size: 30rpx;
	color: #8f8f8f;
	width: 100%;
	text-align: center;
	display: block;
	position: relative;
	z-index: 2;
}

.pass_text {
	width: 50%;
	position: relative;
}

.pass_text:first-child::after {
	content: '';
	width: 380rpx;
	height: 1rpx;
	background-color: #c2c2c2;
	position: absolute;
	left: 54%;
	margin-left: 0;
	top: 0px;
	z-index: 1;
	margin-top: 30rpx;
}

.pass_head {
	overflow: hidden;
	width: 100%;
	background-color: #fafafa;
	border-top: solid 1px #e6e6e6;
	display: flex;
	position: relative;
	padding-top: 40rpx;
	padding-bottom: 40rpx;
}

.pass_head image {
	display: block;
	width: 31rpx;
	height: 110rpx;
	position: absolute;
	left: 50%;
	top: 0px;
	margin-left: -15.5rpx;
	z-index: 0;
}

.pass {
	overflow: hidden;
}
</style>

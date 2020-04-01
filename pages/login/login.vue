<template>
	<view class="login-container">
		<!-- 状态栏 -->
		<uni-nav-bar backgroundColor="#ffe933" :border="false"></uni-nav-bar>
		<!-- 关闭按钮 -->
		<view class="close icon iconfont icon-guanbi pf" @tap="back"></view>
		<view class="head-wrapper">			
			<image class="head-img" src="../../static/common/loginhead.png" mode="widthFix" lazy-load></image>
		</view>
		<view class="login-form setting-container">
			<!-- 手机号验证码登录 -->
			<template v-if="isPhone">
				<view class="pr">
					<view class="phone-pre pa u-f u-f-ac">+86</view>
					<input type="text"  v-model="phone" class="uni-input common-input" placeholder="请输入手机号码" />
				</view>				
				<view class="login-box pr">
					<input type="text" v-model="checknum" class="uni-input common-input" placeholder="请输入验证码" />
					<view class="pa u-f-center yzm-box" @tap="getYZM">
						<view class="yzm">{{codetime == 0 ? '获取验证码' : codetime + 's后获取'}}</view>
					</view>
				</view>		
			</template>
			<!-- 账号密码登录 -->
			<template v-else>
				<input type="text"  v-model="username" class="uni-input common-input" placeholder="昵称/手机号/邮箱" />
				<view class="login-box pr">
					<input type="text" v-model="password" class="uni-input common-input" placeholder="请输入密码" />
					<view class="pa forget u-f u-f-ac" @tap="forgetPassword">忘记密码？</view>
				</view>			
			</template>			
				
			<button type="primary" class="user-setting-btn" :class="{'user-setting-btn-disabled': disabled}" :disabled="disabled"
			:loading="loading" @tap="complete">登录</button>
		</view>
		
		<!-- 登录方式切换 -->
		<view class="login-type u-f-center" @tap="toggleType">{{typeText}}<view class="icon iconfont icon-jinru color-ccc"></view></view>
		
		<!-- 第三方登录 -->
		<view class="other-login-title u-f-center color-ccc">第三方登录</view>
		<other-login></other-login>
		<view class="u-f-center color-ccc">注册即代表您同意<view class="xy">《仿糗事百科用户协议》</view></view>
		
	</view>
</template>

<script>
	import uniNavBar from '../../components/uni-nav-bar/uni-nav-bar.vue'
	import OtherLogin from '../../components/home/other-login.vue'
	export default {
		components: {
			uniNavBar,
			OtherLogin
		},
		data() {
			return {
				loading: false,
				isPhone: true,
				username: '',
				password: '',
				phone: '',
				checknum: '',
				codetime: 0 // 验证码倒计时
			}
		},
		computed: {
			typeText() {
				return this.isPhone ? '账号密码登录' : '验证码登录'
			},
			disabled() {
				if ((this.username && this.password) || (this.phone && this.checknum)) {
					return false
				} else {
					return true
				}
			}
		},
		methods: {
			// 初始化表单
			initForm() {
				this.username = ''
				this.password = ''
				this.phone = ''
				this.checknum = ''
			},
			// 返回
			back() {
				uni.navigateBack({
					delta: 1
				})
			},
			// 登录
			complete() {
				if (this.isPhone) {
					// 验证手机号合法性
					if (!this.checkPhone()) {
						uni.showToast({
							title: '请输入正确手机号',
							icon: 'none'
						})
						return 
					}
				}
			},
			forgetPassword() {
				
			},
			// 校验手机
			checkPhone() {
				let pattern = /^1[34578]\d{9}$/
				return pattern.test(this.phone)
			},
			// 获取验证码
			getYZM() {
				if (this.codetime > 0) {
					uni.showToast({
						title: '不能重复获取',
						icon: 'none'
					})
					return
				} else {
					// 验证手机号合法性					
					if (!this.checkPhone()) {
						uni.showToast({
							title: '请输入正确手机号',
							icon: 'none'
						})
						return 
					}
					this.codetime = 10
					let timer = setInterval(() => {
						this.codetime--
						if (this.codetime < 1) {
							clearInterval(timer)
							this.codetime = 0
						}
					}, 1000)
				}
			},
			toggleType() {
				this.initForm()
				this.isPhone = !this.isPhone
			}
		}
	}
</script>

<style lang="scss" scoped>
@import "../../common/form.scss";


.login-container {
	
	.close {
		left: 40rpx;
		top: 80rpx;
		z-index: 100;
		color: #000;
		font-size: 40rpx;
		font-weight: bold;
	}
	
	.head-wrapper {		
		.head-img {
			width: 100%;
			background: rgba(0, 0, 0, .1);
		}
	}
	
	.login-type {
		padding: 10rpx 0;
	}
	
	.other-login-title {		
		position: relative;
		
		&::before, 
		&::after{
			content: "";
			position: absolute;
			width: 100rpx;
			height: 1rpx;
			background: #CCCCCC;
			top: 50%;
		}
		
		&::before {
			left: 25%;
		}
		
		&::after {
			right:25%;
		}
	}
	
	.login-box {
		width: 100%;
		background-color: red;
		
		input {
			padding-right: 150rpx;
		}		
		
		.yzm {
			width: 100%;
			padding: 8rpx 0;
			text-align: center;
			background: #f4f4f4;
			font-size: 26rpx;
			border-radius: 10rpx;
			color: #CCCCCC;
		}
	}
	
	.phone-pre {
		width: 70rpx;
		height: 100%;		
			
		& + input {
			padding-left: 70rpx;
		}
	}
	
	.forget,
	.yzm-box{
		left: auto;
		right: 0;
		width: 150rpx;	
		height: 100%;
		justify-content: flex-end;
	}
	
	.xy {
		color: #2caefc;
	}
	
}
</style>

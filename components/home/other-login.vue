<template>
	<view class="other-login u-f u-f-ac">
		<block v-for="item in providerList" :key="item.id">
			<view class="u-f-center f1" @tap="tologin(item)">
				<view class="icon iconfont u-f-center" :class="['icon-' + item.icon, item.iconClass]"></view>
			</view>
		</block>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				providerList: []
			}			
		},
		created() {
			this.getAuthLogin()
		},
		methods: {
			getAuthLogin() {
				uni.getProvider({
					service: 'oauth',
					success: (result) => {
						this.providerList = result.provider.map((value, index) => {
							let providerName = '';
							let icon = ''
							let iconClass = ''
							switch (value) {
								case 'weixin':
									providerName = '微信登录'
									icon = 'weixin'
									iconClass = 'wx'
									break;
								case 'qq':
									providerName = 'QQ登录'
									icon = 'QQ'
									iconClass = 'qq'
									break;
								case 'sinaweibo':
									providerName = '新浪微博登录'
									icon = 'xinlangweibo'
									iconClass = 'wb'
									break;						
							}							
							return {
								name: providerName,
								id: value,
								icon,
								iconClass
							}
						});						
						
						this.providerList = this.providerList.filter(item => {
							return item.name !== ''
						})
				
					},
					fail: (error) => {
						console.log('获取登录通道失败', error);
					}
				});
			},
			tologin(provider) {
				uni.login({
					provider: provider.id,
			        // #ifdef MP-ALIPAY
			        scopes: 'auth_user',  //支付宝小程序需设置授权类型
			        // #endif
					success: (res) => {
						console.log('login success:', res);
						// 更新保存在 store 中的登录状态
						// this.login(provider.id);
						uni.showToast({
							title: '登录成功',
							icon: 'success'
						})
					},
					fail: (err) => {
						console.log('login fail:', err);
					}
				});
			}
		}
	}
</script>

<style lang="scss" scoped>
	.other-login {
		padding: 20rpx 80rpx;

		.icon {
			width: 100rpx;
			height: 100rpx;
			border: 1rpx solid;
			border-radius: 100%;
			font-size: 55rpx;
			color: #ffffff;
		}

		.wx {
			background: #2bd198;
		}

		.wb {
			background: #fc7729;
		}

		.qq {
			background: #2caefc;
		}
	}
</style>

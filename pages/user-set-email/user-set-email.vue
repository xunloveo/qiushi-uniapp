<template>
	<view class="setting-container">
		<input type="text"  v-model="email" class="uni-input common-input" placeholder="输入你要绑定的邮箱" />
		<input type="text"  v-model="password" class="uni-input common-input" placeholder="请输入密码" />
		<button type="primary" class="user-setting-btn" :class="{'user-setting-btn-disabled': disabled}" :disabled="disabled"
		:loading="loading" @tap="complete">完成</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				loading: false,
				email: '',
				password: ''
			}
		},
		computed: {
			disabled() {
				if (this.email || this.password) {
					return false
				}
				return true
			}
		},
		methods: {
			// 检验
			check() {
				if (!this.email || this.email === '') {
					uni.showToast({
						title: '邮箱不能为空!',
						icon: 'none'
					})
					return false
				}
				
				// 验证邮箱格式是否正确
				let ePattern = /^([A-Za-z0-9_\-\.])+\@([A-Za-z0-9_\-\.])+\.([A-Za-z]{2,4})$/;
				if (!ePattern.test(this.email)) {
					uni.showToast({
						title: '邮箱格式错误!',
						icon: 'none'
					})
					return false
				}
				
				if (!this.password || this.password === '') {
					uni.showToast({
						title: '密码不能为空!',
						icon: 'none'
					})
					return false
				}
				
				return true
			},
			// 提交事件
			complete() {
				this.loading = true
				this.disabled = true
				if (!this.check()) {
					this.loading = false
					this.disabled = false
					return
				}
				
				setTimeout(() => {
					uni.showToast({
						title: '提交成功！'
					})
					this.loading = false
					this.disabled = false
				}, 2000)
				
			}
		}
	}
</script>

<style lang="scss" scoped>
	@import "../../common/form.scss";
</style>

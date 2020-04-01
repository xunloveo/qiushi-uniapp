<template>
	<view class="setting-container">
		<input type="text" password v-model="oldPassword" class="uni-input common-input" placeholder="输入旧密码" />
		<input type="text" password v-model="newPassword" class="uni-input common-input" placeholder="输入新密码" />
		<input type="text" password v-model="reNewPassword" class="uni-input common-input" placeholder="输入确认密码" />
		<button type="primary" class="user-setting-btn" :class="{'user-setting-btn-disabled': disabled}" :disabled="disabled"
		:loading="loading" @tap="complete">完成</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				loading: false,
				oldPassword: '',
				newPassword: '',
				reNewPassword: ''
			}
		},
		computed: {				
			disabled() {
				if (this.oldPassword || this.newPassword || this.reNewPassword) {
					return false
				}
				return true
			}
		},
		methods: {
			// 检验
			check() {
				if (!this.oldPassword || this.oldPassword === '') {
					uni.showToast({
						title: '旧密码不能为空!',
						icon: 'none'
					})
					return false
				}
				if (!this.newPassword || this.newPassword === '') {
					uni.showToast({
						title: '新密码不能为空!',
						icon: 'none'
					})
					return false
				}
				if (!this.reNewPassword || this.reNewPassword === '') {
					uni.showToast({
						title: '确认密码不能为空!',
						icon: 'none'
					})
					return false
				}
				if (this.reNewPassword !== this.newPassword) {
					uni.showToast({
						title: '确认密码与新密码一致!',
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

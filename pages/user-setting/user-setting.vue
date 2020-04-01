<template>
	<view class="setting-container">
		<block v-for="item in settingList" :key="item">
			<home-list :item="item"></home-list>
		</block>
		<button type="primary" class="user-setting-btn">退出登录</button>
	</view>
</template>

<script>
	import HomeList from '../../components/home/home-list.vue'
	export default {
		components: {
			HomeList
		},
		data() {
			return {
				settingList: [
					{ name: '账号与安全', clickType: 'navigateTo', url: '../user-set-repassword/user-set-repassword' },
					{ name: '绑定邮箱', clickType: 'navigateTo', url: '../user-set-email/user-set-email' },
					{ name: '资料编辑', clickType: 'navigateTo', url: '../user-set-userinfo/user-set-userinfo' },
					{ name: '小纸条', clickType: '', url: '' },
					{ name: '清除缓存', clickType: 'clear', url: '' },
					{ name: '意见反馈', clickType: 'navigateTo', url: '../user-set-help/user-set-help' },
					{ name: '关于仿糗百', clickType: 'navigateTo', url: '../user-set-about/user-set-about' }
				]
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="scss" scoped>
@import  "../../common/form.scss";
</style>

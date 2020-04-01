<template>
	<view class="setting-container">
		<view class="about-info-t u-f-center u-f-col">
			<image src="../../static/common/logo.png" mode="widthFix" lazy-load></image>
			<view>Version 1.0.0</view>
		</view>
		<block v-for="item in settingList" :key="item">
			<home-list :item="item"></home-list>
		</block>
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
					{ name: '新版本检测'},
					{ name: '仿糗事百科用户协议'}					
				]
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="scss" scoped>
@import  "../../common/form.scss";

.about-info-t {
	padding: 40rpx 0;
	
	image {
		margin-top: 50rpx;
		margin-bottom: 30rpx;
		width: 70%;
	}
	
	view {
		color: #cccccc;
	}
}
</style>

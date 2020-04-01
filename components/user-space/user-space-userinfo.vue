<template>
	<view class="user-sapce-userinfo">
		<view class="user-sapce-userinfo-item">
			<view class="title">账号信息</view>
			<view>糗龄：{{getRegTime}}</view>
			<view>糗百ID：{{userinfo.id}}</view>
		</view>
		<view class="user-sapce-userinfo-item">
			<view class="title">个人信息</view>
			<view>星座：{{getXinzuo}}</view>
			<view>职业：{{userinfo.job}}</view>
			<view>故乡：{{userinfo.path}}</view>
			<view>情感状态：{{userinfo.qg}}</view>
		</view>
	</view>
</template>

<script>
	import Time from '../../common/time.js'
	export default {
		props: {
			userinfo: Object
		},
		computed: {
			//计算注册时间
			getRegTime() {
				return Time.gettime.sumAge(this.userinfo.regTime)
			},
			// 计算星座
			getXinzuo() {
				return Time.gettime.getHoroscope(this.userinfo.birthday)
			},
		},
	}
</script>

<style lang="scss" scoped>
	.user-sapce-userinfo {
		padding: 0 20rpx;

		.user-sapce-userinfo-item {
			padding: 15rpx 0;
			color: #CCCCCC;
			border-bottom: 1rpx solid #eeeeee;

			.title {
				padding: 15rpx 0;
				color: #333;
				font-size: 32rpx;
			}

		}
	}
</style>

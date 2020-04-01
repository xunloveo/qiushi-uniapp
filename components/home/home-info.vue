<template>
	<view class="home-info u-f u-f-ac" @tap="goSpace">
		<image :src="homeInfo.userpic" mode="widthFix" lazy-load></image>
		<view class="f1">
			<view class="name">{{homeInfo.username}}</view>
			<view class="visited">总访客 {{homeInfo.totalnum}} 今日 {{homeInfo.todaynum}}</view>
		</view>
		<view class="icon iconfont icon-jinru"></view>
	</view>
</template>

<script>
	export default {
		props: {
			homeInfo: Object
		},
		methods: {
			goSpace() {
				uni.navigateTo({
					url: '../../pages/user-space/user-space'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.home-info {
		padding: 20rpx;

		image {
			flex-shrink: 0;
			width: 100rpx;
			height: 100rpx;
			border-radius: 100%;
			margin-right: 15rpx;
		}

		.icon-jinru {
			height: 100%;
		}

		.name {
			font-size: 32rpx;
		}

		.visited {
			color: #bbbbbb;
		}
	}
</style>

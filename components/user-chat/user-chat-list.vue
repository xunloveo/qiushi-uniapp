<template>
	<view>
		<view v-if="item && item.gstime" class="user-chat-time u-f-center">{{item.gstime}}</view>
		<view class="user-chat-list u-f" :class="[item.isme ? 'user-chat-me' : '']">
			<image v-if="!item.isme" :src="item.userpic" mode="widthFix" lazy-load></image>
			<view class="user-chat-list-content">
				<!-- 文字 -->
				<text v-if="item.type=='text'">{{item.data}}</text>
				<!-- 图片 -->
				<image v-if="item.type=='img'" :src="item.data" mode="widthFix" lazy-load></image>
			</view>
			<image v-if="item.isme" :src="item.userpic" mode="widthFix" lazy-load></image>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index: Number
		}
	}
</script>

<style lang="scss" scoped>
	.user-chat-time {
		padding: 50rpx 0;
		color: #a2a2a2;
		font-size: 24rpx;
	}

	.user-chat-list {
		padding: 20rpx 0;

		image {
			width: 100rpx;
			height: 100rpx;
			border-radius: 100%;
			flex-shrink: 0;
		}

		.user-chat-list-content {
			position: relative;
			background: #f4f4f4;
			padding: 25rpx;
			margin-left: 20rpx;
			margin-right: 100rpx;
			border-radius: 20rpx;

			image {
				max-width: 150rpx;
				max-height: 200rpx;
			}

			&::after {
				content: '';
				width: 0;
				height: 0;
				position: absolute;
				left: -30rpx;
				top: 30rpx;
				right: 0;
				border: 16rpx solid #f4f4f4;
				border-color: transparent #f4f4f4 transparent transparent;
			}
		}

		&.user-chat-me {
			justify-content: flex-end;

			.user-chat-list-content {
				margin-right: 20rpx;
				margin-left: 100rpx;

				&::after {
					left: auto;
					right: -30rpx;
					border-color: transparent transparent transparent #f4f4f4;
				}
			}
		}
	}
</style>

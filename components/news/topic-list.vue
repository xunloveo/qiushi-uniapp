<template>
	<view class="topic-new-list u-f animated fadeIn fast" @tap="openTopicDetail">
		<image :src="item.titlepic" mode="widthFix" lazy-load></image>
		<view>
			<view class="topic-list-title">#{{item.title}}#</view>
			<view>{{item.desc}}</view>
			<view>动态 {{item.totalnum}} 今日 {{item.todaynum}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index: Number
		},
		methods: {
			openTopicDetail() {
				uni.navigateTo({
					url: '../../pages/topic-detail/topic-detail'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.topic-new-list {
		padding: 10rpx 0;
		border-bottom: 1rpx solid #EEEEEE;
		color: #A4A4A4;

		image {
			width: 150rpx;
			height: 150rpx;
			border-radius: 10rpx;
			margin-right: 20rpx;
		}

		.topic-list-title {
			color: #333333;
			font-size: 32rpx;
		}
	}
</style>

<template>
	<view class="topic-nav">
		<view class="u-f u-f-ac u-f-jcsb">
			<view class="topic-nav-title">热门分类</view>
			<view class="u-f u-f-ac" @tap="openTopicNav">更多<view class="icon iconfont icon-jinru"></view></view>
		</view>
		<view class="u-f u-f-ac">
			<block v-for="(item, index) in nav" :key="index">
				<view>{{item.name}}</view>
			</block>								
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			nav: Array
		},
		methods: {
			openTopicNav() {
				uni.navigateTo({
					url: '../../pages/topic-nav/topic-nav'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.topic-nav {
		border-bottom: 1rpx solid #EEEEEE;
		border-top: 1rpx solid #EEEEEE;
		padding: 20rpx;
		
		& > view:first-child {
			margin-bottom: 10rpx;
			color: #9E9E9E;
		}
		
		& > view:last-child {
			view {
				text-align: center;
				flex: 1;
				background: #DDDDDD;
				color: #9E9E9E;
				margin: 0 10rpx;
				border-radius: 10rpx;
			}
		}
		
		.topic-nav-title {
			color: #000000;
			font-size: 32rpx;
		}
		
	}
</style>

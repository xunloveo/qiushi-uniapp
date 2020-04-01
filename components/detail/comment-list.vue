<template>
	<view class="uni-comment-list animated fadeIn fast" :class="{'u-comment-child': item.fid !== 0}">
		<view class="uni-comment-face">
			<image :src="item.userpic" mode="widthFix"></image>
		</view>
		<view class="uni-comment-body">
			<view class="uni-comment-top">
				<text>{{item.username}}</text>
			</view>
			<view class="uni-comment-content">{{item.data}}</view>
			<view class="uni-comment-date">
				<view>{{item.time}}</view>
			</view>
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
	.u-comment {
		padding: 0 20rpx;
	}
	
	.u-comment-child {
		box-sizing: border-box;
		width: auto;
		padding: 20rpx;
		margin: 0;
		margin-left: 70rpx;
		background: #f4f4f4;
		border-bottom: 1px solid #eeeeee;
	}
</style>

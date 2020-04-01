<template>
	<view>
		<!-- 模糊背景 -->
		<view class="topic-bg">
			<image :src="toppicInfo.titlepic" mode="aspectFill" lazy-load></image>
		</view>
		<!-- 话题信息 -->
		<view class="topic-info">
			<view class="topic-info-top u-f u-f-ac">
				<image :src="toppicInfo.titlepic" mode="widthFix" lazy-load></image>
				<view>#{{toppicInfo.title}}#</view>
			</view>
			<view class="topic-info-center u-f">
				<view>动态 {{toppicInfo.totalnum}}</view>
				<view> 今日 {{toppicInfo.todaynum}}</view>
			</view>
			<view class="topic-info-bottom">{{toppicInfo.desc}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			toppicInfo: Object
		}
	}
</script>

<style lang="scss" scoped>
.topic-bg {
	width: 100%;
	height: 300rpx;
	position: relative;
	overflow: hidden;
	
	image {
		width: 100%;
		position: absolute;
		filter: blur(10px);
	}
}

.topic-info {
	padding: 0 25rpx;
	
	.topic-info-top {
		position: relative;
		
		image {
			width: 150rpx;
			height: 150rpx;
			position: absolute;
			top: -75rpx;
			border-radius: 20rpx;
		}
		
		view {
			flex: 1;
			font-size: 35rpx;
			margin-left: 170rpx;
		}
	}
	
	.topic-info-center {
		padding: 35rpx 0 15rpx;
		
		view {
			color: #cdcdcd;
		}
	}
	
	.topic-info-bottom {
		color: #A3A3A3;
		font-size: 32rpx;
		padding-bottom: 10rpx;
	}
}
</style>

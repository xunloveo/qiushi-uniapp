<template>
	<view class="age icon iconfont" :class="[sex === 0 ? 'icon-nan' : 'icon-nv']">{{age}}</view>
</template>

<script>
	export default {
		props: {
			sex: Number,
			age: Number
		}
	}
</script>

<style lang="scss" scoped>
	.age {
		background: #007AFF;
		color: #FFFFFF;
		font-size: 23rpx;
		padding: 5rpx 10rpx;
		margin-left: 10rpx;
		border-radius: 20rpx;
		line-height: 22rpx;
		
		&.icon-nv {
			background: #ff698d;
		}
	}
</style>

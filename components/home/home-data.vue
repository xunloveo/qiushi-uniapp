<template>
	<view class="u-f-center u-f-col">
		<view class="num">{{item.num}}</view>{{item.name}}
	</view>
</template>

<script>
	export default {
		props: {
			item: Object
		}
	}
</script>

<style lang="scss" scoped>
	.num {
		font-size: 32rpx;
		color: #333333;
	}
</style>

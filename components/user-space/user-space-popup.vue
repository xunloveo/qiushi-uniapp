<template>
	<view>
		<view class="paper-menu-popup-mask" v-show="show" @tap="hidePopup"></view>
		<view class="paper-menu-popup" v-show="show">
			<view class="u-f u-f-ac" hover-class="paper-menu-popup__hover" @tap="lahei"><view class="icon iconfont icon-sousuo"></view>拉黑</view>
			<view class="u-f u-f-ac" hover-class="paper-menu-popup__hover" @tap="beizhu"><view class="icon iconfont icon-qingchu"></view>备注</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			show: Boolean
		},
		methods: {
			hidePopup() {
				this.$emit('hide')
			},
			lahei() {
				this.$emit('lahei')
			},
			beizhu() {
				this.$emit('beizhu')
			}
		}
	}
</script>

<style lang="scss" scoped>
	.paper-menu-popup {
		position: fixed;
		right: 0;
		top: 100rpx;
		width: 50%;
		z-index: 2000;
		background: #FFFFFF;
		box-shadow: 1rpx 1rpx 20rpx 2rpx #CCCCCC;
		
		& > view {
			padding: 20rpx;
			font-size: 35rpx;
			
			&.paper-menu-popup__hover {
				background: #EEEEEE;
			}
		}
		
		.icon {
			margin-right: 10rpx;
		}
	}
	
	.paper-menu-popup-mask {
		position: fixed;
		left: 0;
		top: 0;
		right: 0;
		bottom: 0;
		z-index: 1999;
	}
</style>

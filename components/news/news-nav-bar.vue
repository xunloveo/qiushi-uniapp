<template>
	<view>
		<uni-nav-bar fixed :statusBar="true" :border="false" @click-right="openAdd">		
			<block slot="left">
				<view class="nav-left">
					<view class="icon iconfont icon-qiandao"></view>
				</view>
			</block>
			<view class="nav-title u-f-center">
				<block v-for="(item, index) in tabBars" :key="item.id">
					<view class="u-f-center" :class="{'active': tabIndex === index}" @tap="change(index)">
						<text>{{item.name}}</text>
						<view v-if="tabIndex === index" class="nav-title-line"></view>
					</view>
				</block>
			</view>
			<block slot="right">
				<view class="nav-right u-f-center">
					<view class="icon iconfont icon-bianji1"></view>
				</view>
			</block>
		</uni-nav-bar>
	</view>
</template>

<script>
	import uniNavBar from '../uni-nav-bar/uni-nav-bar.vue'
	export default {
		components: {
			uniNavBar
		},
		props: {
			tabBars: Array,
			tabIndex: Number
		},
		methods: {
			// 打开发布页面
			openAdd() {
				uni.navigateTo({
					url: '../add-input/add-input'
				})
			},
			// 点击切换
			change(index) {
				this.$emit('change-tab', index)
			}
		}
	}
</script>

<style lang="scss" scoped>
	.nav-left,
	.nav-right {
		view {
			font-size: 40rpx;
		}
	}
	
	.nav-left {
		margin-left: 16rpx;
	
		view {
			color: #FF9619;
		}
	}
	
	.nav-right {
		width: 100%;
	}
	
	.nav-title {
		height: 100%;
		margin-left: -20rpx;
		width: 100%;
	
		&>view {
			font-size: 32rpx;
			padding: 0 15rpx;
			font-weight: bold;
			color: #969696;
	
			&.active {
				color: #333333;
	
				.nav-title-line {
					position: absolute;
					bottom: 12rpx;
					width: 70rpx;
					height: 10rpx;
					background: #FEDE33;
					border-radius: 20rpx;
				}
			}
		}
	}
</style>

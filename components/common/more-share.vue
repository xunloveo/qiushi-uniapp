<template>
	<view class="animated fadeIn faster" v-if="show">
		<!-- 分享 -->
		<view class="more-share-model" @tap="toggleShareShow"></view>
		<view class="more-share">
			<view class="more-share-title">分享到</view>
			<scroll-view scroll-x class="more-share-body u-f-center">
				<block v-for="(val, index) in providerList" :key="index">
					<view class="more-share-item" hover-class="more-share-hover" @tap="share(val)">
						<view class="icon iconfont icon-weixin u-f-center more-share-wx" :class="['icon-' + val.icon, 'more-share-'+val.class]"></view>
						<view class="text">{{val.name}}</view>
					</view>
				</block>
			</scroll-view>
			<view class="more-share-bottom" @tap="toggleShareShow">取消</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			show: Boolean,
			providerList: Array
		},
		methods: {
			toggleShareShow() {
				this.$emit('toggle', !this.show)
			},
			share(val) {
				this.$emit('share', val)
			}
		}
	}
</script>

<style lang="scss" scoped>
	// 分享样式
	.more-share-model {
		position: fixed;
		left: 0;
		right: 0;
		top: 0;
		bottom: 0;
		z-index: 100;
		background: rgba(51, 51, 51, .43);
	}

	.more-share {
		position: fixed;
		left: 0;
		bottom: 0;
		right: 0;
		z-index: 110;
		background: #ffffff;

		.more-share-title,
		.more-share-bottom {
			padding: 25rpx;
			font-size: 32rpx;
			text-align: center;
		}

		.more-share-body {
			white-space: nowrap;
			width: 100%;
			height: 200rpx;
			border-bottom: 1rpx solid #eeeeee;

			.more-share-item {
				width: 25%;
				height: 200rpx;
				line-height: 200rpx;
				display: inline-flex;
				justify-content: center;
				align-items: center;
				flex-direction: column;

				.icon {
					width: 100rpx;
					height: 100rpx;
					font-size: 55rpx;
					border-radius: 100%;
					color: #fff;
				}

				.text {
					color: #7a7a7a;
				}
			}

			.more-share-hover {
				background: #eeeeee;
			}

			.more-share-wx {
				background: #2ad19b;
			}

			.more-share-pyq {
				background: #514d4c;
			}

			.more-share-wb {
				background: #ee5e5e;
			}

			.more-share-qq {
				background: #4a73ba;
			}
		}
	}
</style>

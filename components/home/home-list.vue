<template>
	<view class="home-list-item u-f u-f-ac u-f-jcsb" hover-class="item-hover" @tap="handleEvent">
		<view class="u-f u-f-ac">
			<view v-if="item.icon" class="icon iconfont" :class="['icon-' + item.icon]" :style="{color: item.color}"></view>{{item.name}}
		</view>
		<view class="icon iconfont icon-jinru"></view>
	</view>
</template>

<script>
	export default {
		props: {
			item: Object,
			index: Number
		},
		methods: {
			handleEvent() {
				switch (this.item.clickType) {
					case 'navigateTo':
						if (this.item.url) {
							uni.navigateTo({
								url: this.item.url
							})
						}
						break;
					case 'clear':
						uni.showModal({
							title: '',
							content: '是否清除缓存？',							
							cancelText: '取消',
							confirmText: '清除缓存',
							success(res) {
								if (res.confirm) {
									uni.clearStorage()
									uni.showToast({
										title: '清除缓存成功'
									})
								}
							}
						})
						break;
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.home-list-item {
		padding: 20rpx;
		border: 1rpx solid #eeeeee;
		border-left: 0;
		border-right: 0;

		&.item-hover {
			background: #f4f4f4;
		}

		&>view:first-child {
			color: #333333;

			.icon {
				margin-right: 10rpx;
			}
		}

		&>view:last-child {
			color: #cccccc;
		}
	}
</style>

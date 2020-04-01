<template>
	<view class="space-head u-f-center">
		<image :src="getBgimg" mode="widthFix" lazy-load class="bgimg" @tap.stop="changeBgImg"></image>
		<view class="u-f-center u-f-col head-info">
			<image :src="userinfo.userpic" mode="widthFix" lazy-load class="avatar"></image>
			<view class="u-f-center mr15-tb title">{{userinfo.username}}
				<tag-sex-age :age="userinfo.age" :sex="userinfo.sex"></tag-sex-age>
			</view>
			<view class="icon iconfont u-f-center guangzhu mr15-tb" :class="[isguangzhu ? 'active' : 'icon-zengjia']" @tap="toggleGuangzhu">{{isguangzhu ? '已关注' : '关注'}}</view>
		</view>
	</view>
</template>

<script>
	import TagSexAge from '../common/tag-sex-age.vue'
	export default {
		components: {
			TagSexAge
		},
		props: {
			userinfo: Object
		},
		data() {
			return {
				isguangzhu: this.userinfo.isguangzhu
			}
		},
		computed: {
			getBgimg() {
				return `../../static/bgimg/${this.userinfo.bgimg}.jpg`
			}
		},
		methods: {
			// 切换关注
			toggleGuangzhu() {
				this.isguangzhu = !this.isguangzhu
			},
			// 切换背景图
			changeBgImg() {
				let num = this.userinfo.bgimg
				num = num < 4 ? ++num : 1
				this.userinfo.bgimg = num
			}
		}
	}
</script>

<style lang="scss" scoped>
	.space-head {
		position: relative;
		height: 500rpx;
		overflow: hidden;

		.bgimg {
			width: 100%;
		}

		.avatar {
			width: 150rpx;
			height: 150rpx;
			border-radius: 100%;
		}

		.head-info {
			position: absolute;
			top: 150rpx;

			.title {
				color: #fff;
				font-size: 35rpx;
				font-weight: bold;

				.age {
					border: 2rpx solid #fff;
				}
			}

			.guangzhu {
				background: #ffe933;
				color: #333;
				border: solid 1rpx #ffe933;
				padding: 0 15rpx;
				border-radius: 10rpx;
				font-size: 28rpx;

				&.active {
					background: none;
					color: #fff;
					border-color: #fff;
				}
			}
		}
	}
</style>

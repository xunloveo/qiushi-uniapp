<template>
	<view class="index-list animated fadeIn fast">
		<view class="index-list1 u-f u-f-ac u-f-jcsb">
			<view class="u-f u-f-ac">
				<image :src="item.userpic" mode="widthFix" lazy-load></image>
				{{item.username}}
			</view>
			<view class="u-f u-f-ac" v-show="!isGuangzhu" @tap="guanzhu">
				<view class="icon iconfont icon-zengjia"></view>关注
			</view>
		</view>
		<view class="index-list2" @tap="openDetail">{{item.title}}</view>
		<view class="index-list3 u-f-center">
			<image :src="item.titlepic" mode="widthFix" lazy-load @tap="openDetail"></image>
			<!-- 视频 -->
			<view class="index-list-play icon iconfont icon-bofang" v-if="item.type === 'video'"></view>
			<view class="index-list-playinfo" v-if="item.type === 'video'">
				{{item.playnum}}次播放 {{item.long}}
			</view>
		</view>
		<view class="index-list4 u-f u-f-ac u-f-jcsb">
			<view class="u-f u-f-ac">
				<view class="u-f u-f-ac" :class="{'active': infonum.index === 1}" @tap="operator(1)">
					<view class="icon iconfont icon-icon_xiaolian-mian"></view><text>{{infonum.dingnum}}</text>
				</view>
				<view class="u-f u-f-ac" :class="{'active': infonum.index === 2}" @tap="operator(2)">
					<view class="icon iconfont icon-kulian"></view><text>{{infonum.cainum}}</text>
				</view>
			</view>
			<view class="u-f u-f-ac">
				<view class="u-f u-f-ac">
					<view class="icon iconfont icon-pinglun1"></view>{{item.commentnum}}
				</view>
				<view class="u-f u-f-ac">
					<view class="icon iconfont icon-zhuanfa"></view>{{item.sharenum}}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			item: {
				type: Object
			},
			index: {
				type: Number
			}
		},	
		data() {
			return {
				isGuangzhu: this.item.isGuangzhu,
				infonum: this.item.infonum
			}
		},
		methods: {
			// 关注
			guanzhu() {
				this.isGuangzhu = true
				uni.showToast({
					title: '关注成功！'
				});
			},
			// 哭脸笑脸操作
			operator(type) {
				switch (type) {
					case 1:
						// 如果已经顶过了
						if (this.infonum.index === 1) return
						// 如果是没顶过的		
						this.infonum.dingnum++						
						// 如果踩过 就需要减1
						if (this.infonum.index === 2) {
							this.infonum.cainum--
						}
						this.infonum.index = 1						
						break;
					case 2:
						// 如果已经踩过了
						if (this.infonum.index === 2) return
						// 如果是没顶过的						
						this.infonum.cainum++
						// 如果踩过 就需要减1
						if (this.infonum.index === 1) {
							this.infonum.dingnum--
						}
						this.infonum.index = 2						
						break;
				}
			},
			// 跳转到详情页
			openDetail() {
				uni.navigateTo({
					url: `../../pages/detail/detail?detailData=${JSON.stringify(this.item)}`,
				});
			}
		}
	}
</script>

<style lang="scss" scoped>
	.index-list {
		padding: 20rpx;
		border-bottom: 1rpx solid #EEEEEE;

		.index-list1 {

			&>view {

				&:first-child {
					color: #999999;
				}

				&:last-child {
					background-color: #F4F4F4;
					border-radius: 5rpx;
					padding: 0 10rpx;
				}
			}

			image {
				width: 90rpx;
				height: 90rpx;
				border-radius: 100%;
				margin-right: 10rpx;
			}
		}

		.index-list2 {
			padding-top: 15rpx;
			font-size: 32rpx;
		}

		.index-list3 {
			position: relative;
			padding-top: 15rpx;

			image {
				width: 100%;
				border-radius: 20rpx;
			}

			.index-list-play {
				position: absolute;
				font-size: 140rpx;
				color: #FFFFFF;
			}

			.index-list-playinfo {
				position: absolute;
				padding: 0 12rpx;
				background: rgba(51, 51, 51, 0.72);
				color: #FFFFFF;
				font-size: 22rpx;
				bottom: 8rpx;
				right: 8rpx;
				border-radius: 40rpx;
			}
		}

		.index-list4 {
			padding: 15rpx 0;
			color: #999999;

			&>view {
				&>view {
					margin-right: 10rpx;

					&>view {
						margin-right: 10rpx;
					}
				}
			}

			.active {
				view, text {
					color: #55ff00;
				}
			}
		}
	}
</style>

<template>
	<view class="paper-list u-f u-f-ac animated fadeIn fast" @tap="openChat">
		<image :src="item.userpic" mode="widthFix" lazy-load></image>
		<view class="paper-info">
			<view class="u-f u-f-ac u-f-jcsb"><text class="title">{{item.username}}</text><view class="time">{{item.time}}</view></view>
			<view class="u-f u-f-ac u-f-jcsb">{{item.data}}
				<template v-if="item.noreadnum > 0">
					<uni-badge :text="item.noreadnum" type="error"></uni-badge>
				</template>						
			</view>
		</view>
	</view>		
</template>

<script>	
	import uniBadge from '../uni-badge/uni-badge.vue'
	export default {
		components: {
			uniBadge
		},
		props: {
			item: Object,
			index: Number
		},
		methods: {
			// 跳到聊天页
			openChat() {
				uni.navigateTo({
					url: '../../pages/user-chat/user-chat'
				});
			}
		}
	}
</script>

<style lang="scss" scoped>
	.paper-list {
		padding: 20rpx 0;
		border-bottom: 1rpx solid #EEEEEE;
		
		image {
			width: 100rpx;
			height: 100rpx;
			border-radius: 100%;
			margin-right: 20rpx;
			flex-shrink: 0;
		}
		
		.paper-info {
			flex: 1;
			
			& > view:last-child {
				color: #999999;
			}
			
			.title {
				font-size: 35rpx;
			}		
				
			.time {				
				color: #CBCBCB;
			}
		}
	}
</style>

<template>
	<view class="user-list u-f u-f-ac animated fadeIn fast">
		<image :src="item.userpic" mode="widthFix" lazy-load></image>
		<view class="user-list-text">
			<view class="title">{{item.username}}</view>
			<tag-sex-age :sex="item.sex" :age="item.age" style="display: inline-block;"></tag-sex-age>
		</view>
		<view class="chose icon iconfont u-f u-f-ac" :class="[item.isguangzhu ? 'icon-xuanze-yixuan' : 'icon-zengjia1']"></view>
	</view>
</template>

<script>	
	import TagSexAge from '../common/tag-sex-age.vue'
	export default {
		props: {
			item: Object,
			index: Number
		},
		components: {
			TagSexAge
		}
	}
</script>

<style lang="scss" scoped>
	.user-list {
		padding: 20rpx 0;
		border-bottom: 1rpx solid #EEEEEE;
	
		image {
			width: 100rpx;
			height: 100rpx;
			border-radius: 100%;
			margin-right: 20rpx;
			flex-shrink: 0;
		}
	
		.user-list-text {
			flex: 1;
			
			.title {
				font-size: 35rpx;				
			}
		}
	
		.chose {
			width: 80rpx;
			text-align: center;
			color: #CCCCCC;
			
			&.icon-zengjia1 {
				color: #f8791b;
			}
		}
	}
</style>

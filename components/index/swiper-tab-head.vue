<template>
	<view class="uni-tab-bar">
		<scroll-view scroll-x="true" class="uni-swiper-tab" :style="scrollViewStyle">
			<block v-for="(tab, index) in tabBars" :key="tab.id">
				<view class="swiper-tab-list" :style="scrollViewItemStyle" :class="{'active': tabIndex === index}" @tap="tabtap(index)">
					{{tab.name}} {{tab.num ? tab.num : ''}}
					<view class="swiper-tab-line"></view>
				</view>
			</block>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		props: {
			tabBars: Array,
			tabIndex: Number,
			scrollViewStyle: Object,
			scrollViewItemStyle: Object
		},
		methods: {
			tabtap(index) {
				this.$emit('tabtap', index)
			}
		}
	}
</script>

<style lang="scss" scoped>
	/deep/.uni-scroll-view::-webkit-scrollbar {
			/* 隐藏滚动条，但依旧具备可以滚动的功能 */
			display: none
		}
	
	.uni-swiper-tab {		 
		border-bottom: 1rpx solid #EEEEEE;	
	}	
	
	
	.swiper-tab-list {
		color: #969696;
		font-weight: bold;
	
		&.active {
			color: #343434;
	
			.swiper-tab-line {
				border-bottom: 6rpx solid #FEDE33;
				width: 70upx;
				margin: auto;
				border-top: 6rpx solid #FEDE33;
				border-radius: 20upx;
			}
		}
	}
</style>

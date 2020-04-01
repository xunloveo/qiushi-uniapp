<template>
	<view class="user-chat-bottom u-f u-f-ac animated fadeInDown fast">
		<input type="text" placeholder="文明发言" v-model="text"/>
		<view class="icon iconfont icon-fabu u-f-center" @tap="send"></view>
	</view>
</template>

<script>
	export default {
		data () {
			return {
				text: ''
			}
		},
		methods: {
			// 发送信息
			send() {
				this.$emit('send', this.text)
				this.text = ''
			}
		}
	}
</script>

<style lang="scss" scoped>
	.user-chat-bottom {
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		height: 120upx;
		padding: 0 20rpx;
		background: #fff;
		border-top: 1rpx solid #eeeeee;	
			
		input {
			flex: 1;
			margin-right: 20rpx;
			padding: 10rpx 20rpx;
			border-radius: 10rpx;
			background: #F7F7F7;
		}
		
		view {
			width: 80rpx;
			font-size: 45rpx;
		}
	}
</style>

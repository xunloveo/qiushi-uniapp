<template>
	<view class="common-list u-f animated fadeIn fast">
		<view class="common-list-left">
			<image :src="item.userpic" mode="widthFix" lazy-load></image>
		</view>
		<view class="common-list-right">
			<view class="u-f u-f-c u-f-jcsb">
				<view class="u-f u-f-ac">
					<text class="username">{{item.username}}</text>
					<tag-sex-age :sex="item.sex" :age="item.age"></tag-sex-age>
				</view>
				<view class="u-f-center">
					<view class="gaungzhu icon iconfont icon-zengjia" v-if="!isguangzhu" @tap="guangzhu">关注</view>
				</view>				
			</view>
			<view class="title">{{item.title}}</view>
			<view class="image-wrapper u-f-center">
				<!-- 图片 -->
				<image v-if="item.titlepic" :src="item.titlepic" mode="widthFix" lazy-load></image>
				<!-- 视频 -->
				<template v-if="item.video">
					<view class="common-list-play icon iconfont icon-bofang"></view>
					<view class="common-list-playinfo">
						{{item.video.looknum}} 次播放 {{item.video.long}}
					</view>
				</template>
				<!-- 分享样式 -->
				<view class="common-list-share u-f u-f-ac" v-if="item.share">
					<image :src="item.share.titlepic" mode="widthFix" lazy-load></image>
					<view>{{item.share.title}}</view>
				</view>
			</view>
			<view class="u-f u-f-c u-f-jcsb">
				<view>{{item.path}}</view>
				<view class="u-f u-f-c">
					<view class="icon iconfont icon-zhuanfa"><text>{{item.sharenum}}</text></view>
					<view class="icon iconfont icon-pinglun1"><text>{{item.commentnum}}</text></view>
					<view class="icon iconfont icon-dianzan1"><text>{{item.goodnum}}</text></view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import TagSexAge from './tag-sex-age.vue'
	export default {
		props: {
			item: Object,
			index: Number
		},
		components: {
			TagSexAge
		},
		data() {
			return {
				isguangzhu: this.item.isguangzhu
			}
		},
		methods: {
			guangzhu() {
				this.isguangzhu = true
				uni.showToast({
					title: '关注成功！'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
@import '../../common/list.scss'
</style>

<template>
	<view>
		<!-- 未登录 -->
		<template v-if="!isLogin">
			<view class="u-f-center">登陆仿糗百，体验更多功能</view>
			<!-- 第三方登陆 -->
			<other-login></other-login>
			<!-- 账号密码登录 -->
			<view class="u-f-center" @tap="goLogin">账号密码登陆<view class="icon iconfont icon-jinru"></view>
			</view>
		</template>

		<!-- 登陆 -->
		<template v-else>
			<home-info :home-info="homeInfo"></home-info>
		</template>

		<!-- 数据 -->
		<view class="home-data u-f-center">
			<block v-for="item in homeData" :key="item.name">
				<home-data :item="item" class="f1"></home-data>
			</block>
		</view>
		<!-- 广告位 -->
		<view class="home-ad u-f-center">
			<image src="../../static/demo/datapic/13.jpg" mode="widthFix" lazy-load></image>
		</view>
		<!-- 功能列表 -->
		<view class="home-list">
			<block v-for="(item, index) in list" :key="index">
				<home-list :item="item" :index="index"></home-list>
			</block>			
		</view>


	</view>
</template>

<script>
	import HomeList from '../../components/home/home-list.vue'
	import HomeData from '../../components/home/home-data.vue'
	import HomeInfo from '../../components/home/home-info.vue'
	import OtherLogin from '../../components/home/other-login.vue'
	export default {
		components: {
			HomeList,
			HomeData,
			HomeInfo,
			OtherLogin
		},
		data() {
			return {
				isLogin: true,
				homeInfo: {
					userpic: '../../static/demo/userpic/10.jpg',
					username: '昵称',
					totalnum: 0,
					todaynum: 0
				},
				homeData: [
					{
						name: '糗事',
						num: 0
					},
					{
						name: '动态',
						num: 0
					},
					{
						name: '评论',
						num: 0
					},
					{
						name: '收藏',
						num: 0
					}
				],
				list: [
					{
						name: '浏览历史',
						icon: 'liulan',
						color: '#2DA9FF',
						clickType: '',
						url: ''
					},
					{
						name: '糗百认证',
						icon: 'huiyuanvip',
						color: '#FF7434',
						clickType: '',
						url: ''
					},
					{
						name: '审核糗事',
						icon: 'icon_im_keyboard',
						color: '#2DA9FF',
						clickType: '',
						url: ''
					}
				]
			}
		},
		methods: {
			// 去登陆
			goLogin() {
				uni.navigateTo({
					url: '../login/login'
				})
			}
		},
		onNavigationBarButtonTap(e) {
			if (e.index == 0) {
				uni.navigateTo({
					url: '../user-setting/user-setting'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.home-data {
		padding: 20rpx 40rpx;
		color: #989898;
	}
	
	.home-ad {
		padding: 20rpx;
	
		image {
			width: 100%;
			border-radius: 20rpx;
			height: 150rpx;
		}
	}
	
	.home-list {
		padding: 20rpx;
	}
</style>
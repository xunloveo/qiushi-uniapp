<template>
	<view class="space-container">
		<!-- 背景图 用户信息 -->
		<user-space-head :userinfo="userinfo"></user-space-head>
		<!-- 统计 -->
		<view class="user-space-data u-f u-f-ac">
			<block v-for="item in homeData" :key="item.name">
				<home-data :item="item" class="f1"></home-data>
			</block>
		</view>
		<!-- 分割线 -->
		<view class="line"></view>
		<!-- tab导航 -->
		<!-- tab切换 -->
		<swiper-tab-head :tab-bars="tabBars" :tab-index="tabIndex" scrollViewStyle="border: 0" scrollViewItemStyle="width: 33.33%"
		 @tabtap="tabtap" class="my-tab"></swiper-tab-head>

		<!-- 主页内容 -->

		<template v-if="tabIndex==0">
			<user-space-userinfo :userinfo="userinfo"></user-space-userinfo>
		</template>
		<template v-else>
			<block v-for="(list,listindex) in tabList[tabIndex].list" :key="listindex">
				<common-list :item="list" :index="listindex"></common-list>
			</block>
			<load-more :load-text="tabList[tabIndex].loadText"></load-more>
		</template>
		
		<!-- 弹窗 -->
		<user-space-popup :show="show" @lahei="lahei" @beizhu="beizhu" @hide="hidePopup"></user-space-popup>
	</view>
</template>

<script>
	import UserSpaceHead from '../../components/user-space/user-space-head.vue'
	import HomeData from '../../components/home/home-data.vue'
	import SwiperTabHead from '../../components/index/swiper-tab-head.vue'
	import UserSpaceUserinfo from '../../components/user-space/user-space-userinfo.vue'
	import CommonList from '../../components/common/common-list.vue'
	import LoadMore from '../../components/common/load-more.vue'
	import UserSpacePopup from '../../components/user-space/user-space-popup.vue'
	export default {
		components: {
			UserSpaceHead,
			HomeData,
			SwiperTabHead,
			UserSpaceUserinfo,
			CommonList,
			LoadMore,
			UserSpacePopup
		},
		data() {
			return {
				show: false,
				userinfo: {
					id: 1215,
					bgimg: 1,
					username: '昵称',
					userpic: '../../static/demo/userpic/1.jpg',
					age: 20,
					sex: 0,
					isguangzhu: false,
					regTime: '2020-01-01',
					birthday: '1996-04-01',
					job: 'IT',
					path: '江西南昌',
					qg: '未婚'
				},
				homeData: [{
						name: '获赞',
						num: "10k"
					},
					{
						name: '关注',
						num: 11
					},
					{
						name: '粉丝',
						num: 12
					}
				],
				tabIndex: 0,
				tabBars: [{
						name: '主页',
						id: 'home'
					},
					{
						name: '糗事',
						id: 'qiushi'
					},
					{
						name: '动态',
						id: 'dongtai'
					}
				],
				tabList: [{}, {
						loadText: '加载更多...',
						list: [
							// 文字
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈",
								sex: 0, //0 男 1 女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "",
								video: false,
								share: false,
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20
							},
							// 图文
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈",
								sex: 0, //0 男 1 女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "../../static/demo/datapic/13.jpg",
								video: false,
								share: false,
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20
							},
							// 视频
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈",
								sex: 0, //0 男 1 女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "../../static/demo/datapic/13.jpg",
								video: {
									looknum: "20w",
									long: "2:47"
								},
								share: false,
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20
							},
							// 分享
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈",
								sex: 0, //0 男 1 女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "",
								video: false,
								share: {
									title: "我是分享的标题",
									titlepic: "../../static/demo/datapic/14.jpg"
								},
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20
							},
						]
					},
					{
						loadText: '加载更多...',
						list: [
							// 图文
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈",
								sex: 0, //0 男 1 女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "../../static/demo/datapic/13.jpg",
								video: false,
								share: false,
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20
							},
							// 文字
							{
								userpic: "../../static/demo/userpic/12.jpg",
								username: "哈哈",
								sex: 0, //0 男 1 女
								age: 25,
								isguanzhu: false,
								title: "我是标题",
								titlepic: "",
								video: false,
								share: false,
								path: "深圳 龙岗",
								sharenum: 20,
								commentnum: 30,
								goodnum: 20
							}
						]
					}
				]
			}
		},
		methods: {
			hidePopup() {
				this.show = false
			},
			lahei() {
				this.hidePopup()
			},
			beizhu() {
				this.hidePopup()
			},
			tabtap(index) {
				this.tabIndex = index
			},
			// 上拉加载
			loadMore() {
				console.log(this.tabIndex, 222)
				if (this.tabList[this.tabIndex].loadText != '加载更多...') return
				this.tabList[this.tabIndex].loadText = '加载中...'
				setTimeout(() => {
					let obj = this.tabList[this.tabIndex].list[0]
					this.tabList[this.tabIndex].list.push(obj)
					if (this.tabList[this.tabIndex].list.length == 10) {
						this.tabList[this.tabIndex].loadText = '已经触底了...'
						return
					}
					this.tabList[this.tabIndex].loadText = '加载更多...'

				}, 1000)

			},
		},
		// 上拉加载
		onReachBottom() {
			this.loadMore()
		},
		onNavigationBarButtonTap(e) {
			if(e.index == 0) {
				this.show = true
			}
		}
	}
</script>

<style lang="scss" scoped>
	.space-container {
		.user-space-data {
			background: #ffffff;
			position: relative;
			z-index: 10;
			border-top-left-radius: 20rpx;
			border-top-right-radius: 20rpx;
			margin-top: -15rpx;
		}

		.line {
			height: 20rpx;
			background: #f4f4f4;
		}

	}
</style>

<style lang="scss">
	/* #ifdef MP-WEIXIN */
	.space-container {
		.uni-swiper-tab {
			.swiper-tab-list {
				width: 33.33%;
			}
		}
	}

	/* #endif */
</style>

<template>
	<view>
		<!-- 自定义导航 -->
		<news-nav-bar :tab-bars="tabBars" :tab-index="tabIndex" @change-tab="change"></news-nav-bar>
		<!-- 列表 -->		
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{'height': swiperHeight + 'px'}" :current="tabIndex" @change="tabChange">
				<!-- 关注 -->
				<swiper-item>
					<scroll-view scroll-y="true" class="list" @scrolltolower="loadMore">
						<template v-if="guangzhu.list.length > 0">
							<block v-for="(item, index) in guangzhu.list" :key="index">
								<common-list :item="item" :index="index"></common-list>
							</block>
							<!-- 上拉加载 -->
							<load-more :load-text="guangzhu.loadText"></load-more>
						</template>
						<template v-else>
							<nothing></nothing>
						</template>
					</scroll-view>
				</swiper-item>
				<!-- 话题 -->
				<swiper-item>
					<scroll-view scroll-y="true" class="list">
						<!-- 搜索框 -->
						<view class="search-input">
							<input type="text" class="uni-input" placeholder="搜索内容" placeholder-class="icon iconfont icon-sousuo topic-search" >
						</view>
						<!-- 轮播图 -->
						<swiper class="topic-swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
							<block v-for="item in topic.swiper" :key="item.src">
								<swiper-item>
									<image :src="item.src" mode="widthFix" lazy-load></image>
								</swiper-item>
							</block>
						</swiper>
						<!-- 热门分类 -->
						<news-topic-nav :nav="topic.nav"></news-topic-nav>
						<!-- 最近更新 -->
						<view class="topic-new">
							<view class="topic-new-title">最近更新</view>
							<block v-for="(item, index) in topic.list" :key="index">
								<topic-list :item="item" :index="index"></topic-list>
							</block>							
						</view>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import NewsNavBar from '../../components/news/news-nav-bar.vue'
	import CommonList from '../../components/common/common-list.vue'
	import LoadMore from '../../components/common/load-more.vue'
	import Nothing from '../../components/common/no-thing.vue'
	import NewsTopicNav from '../../components/news/news-topic-nav.vue'
	import TopicList from '../../components/news/topic-list.vue'
	export default {
		components: {
			NewsNavBar,
			CommonList,
			LoadMore,
			Nothing,
			NewsTopicNav,
			TopicList
		},
		data() {
			return {
				topic: {
					swiper: [
						{ src: '../../static/demo/banner1.jpg'},
						{ src: '../../static/demo/banner2.jpg'},
						{ src: '../../static/demo/banner3.jpg'}
					],
					nav: [
						{name: '最新'},
						{name: '游戏'},
						{name: '打卡'},
						{name: '情感'},
						{name: '故事'},
						{name: '喜爱'}
					],
					list: [
						{
							titlepic: '../../static/demo/topicpic/13.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: '../../static/demo/topicpic/12.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						},
						{
							titlepic: '../../static/demo/topicpic/11.jpeg',
							title: '话题名称',
							desc: '我是话题描述',
							totalnum: 50,
							todaynum: 10
						}
					]
				},
				guangzhu: {
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
				swiperHeight: 500,
				tabIndex: 1,
				tabBars: [{
						name: '关注',
						id: 'guanzhu'
					},
					{
						name: '话题',
						id: 'huati'
					}
				]
			}
		},
		methods: {
			// 点击改变
			change(index) {
				this.tabIndex = index
			},
			// 滑动改变
			tabChange(e) {
				this.tabIndex = e.target.current || e.detail.current
			},
			// 上拉加载
			loadMore() {
				if (this.guangzhu.loadText != '加载更多...') return
				this.guangzhu.loadText = '加载中...'
				setTimeout(() => {
					let obj = this.guangzhu.list[Math.floor(Math.random() * 4)]
					this.guangzhu.list.push(obj)
					if (this.guangzhu.list.length == 8) {
						this.guangzhu.loadText = '已经触底了...'
						return
					}
					this.guangzhu.loadText = '加载更多...'
				}, 1000)

			},
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res) => {
					this.swiperHeight = res.windowHeight - uni.upx2px(100)
				}
			})
		},
	}
</script>

<style lang="scss">
	/* #ifdef MP-WEIXIN */

	.uni-status-bar {
		height: 0 !important;
	}	

	/* #endif */
	
	.search-input {
		.topic-search {
			display: flex;
			justify-content: center;
			font-size: 27rpx;
		}
	}
	
</style>

<style lang="scss" scoped>
	.search-input {
		padding: 20rpx;
		
		input {
			background: #F4F4F4;
			border-radius: 10rpx;
		}
	}
	
	.topic-swiper {
		padding: 0 20rpx 20rpx;
		
		image {
			width: 100%;
			height: 150rpx;
			border-radius: 10rpx;
		}
	}
	
	.topic-new {
		padding: 20rpx;
		
		.topic-new-title {
			padding-bottom: 10rpx;
			font-size: 32rpx;
		}
	}
		
</style>

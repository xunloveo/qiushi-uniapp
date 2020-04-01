<template>
	<view class="tabs">
		<!-- 顶部导航栏 -->
		<swiper-tab-head :tab-bars="tabBars" :tab-index="tabIndex" @tabtap="tabtap"></swiper-tab-head>
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{'height': swiperHeight + 'px'}" :current="tabIndex" @change="tabChange">
				<swiper-item v-for="(items, index) in newsList" :key="index">
					<scroll-view scroll-y="true" class="list" @scrolltolower="loadMore(index)">
						<template v-if="items.list.length > 0">
							<!-- 图文列表 -->
							<view class="topic-view">
								<block v-for="(item, index1) in items.list" :key="index1">
									<topic-list :item="item" :index="index1"/>
								</block>
							</view>							
							<!-- 上拉加载 -->
							<load-more :load-text="items.loadText"></load-more>
						</template>
						<template v-else>
							<nothing></nothing>
						</template>
			
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import TopicList from '../../components/news/topic-list.vue'
	import SwiperTabHead from '../../components/index/swiper-tab-head.vue'
	import LoadMore from '../../components/common/load-more.vue'
	import Nothing from '../../components/common/no-thing.vue'

	export default {
		components: {
			TopicList,
			SwiperTabHead,
			LoadMore,
			Nothing
		},
		data() {
			return {
				swiperHeight: 500,
				tabIndex: 0,
				tabBars: [{
					name: '最新',
					id: 'zuixin'
				}, {
					name: '游戏',
					id: 'youxi'
				}, {
					name: '打卡',
					id: 'daka'
				}, {
					name: '情感',
					id: 'qinggan'
				}, {
					name: '故事',
					id: 'gushi'
				}, {
					name: '真爱',
					id: 'zhenai'
				}],
				newsList: [{
						loadText: '加载更多...',
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
							},
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
							},
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
					{
						loadText: '加载更多...',
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
					{
						loadText: '加载更多...',
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
					{
						loadText: '加载更多...',
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
					{
						loadText: '加载更多...',
						list: []
					},
					{
						loadText: '加载更多...',
						list: []
					},
				],

			}
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res) => {
					this.swiperHeight = res.windowHeight - uni.upx2px(100)
				}
			})
		},
		// 监听搜索框点击
		onNavigationBarSearchInputClicked() {
			console.log('ss')
			// 跳到搜索框页面
			uni.navigateTo({
				url: '../search/search'
			})
		},
		// 监听原生标题栏按钮点击事件
		onNavigationBarButtonTap(e) {
			switch (e.index) {
				case 1:
					uni.navigateTo({
						url: '../add-input/add-input'
					})
					break;
			}
		},
		methods: {
			// 上拉加载
			loadMore(index) {
				if (this.newsList[index].loadText != '加载更多...') return
				this.newsList[index].loadText = '加载中...'
				setTimeout(() => {
					let obj = this.newsList[0].list[0]
					this.newsList[index].list.push(obj)
					if (this.newsList[index].list.length == 15) {
						this.newsList[index].loadText = '已经触底了...'
						return
					}
					this.newsList[index].loadText = '加载更多...'

				}, 1000)

			},
			tabtap(index) {
				this.tabIndex = index
			},
			tabChange(e) {
				this.tabIndex = e.target.current || e.detail.current
			}			
		}
	}
</script>

<style scoped>
	.topic-view {
		padding: 0 20rpx;
	}
</style>

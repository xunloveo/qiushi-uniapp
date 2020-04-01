<template>
	<view class="tabs uni-tab-bar">
		<!-- 顶部导航栏 -->
		<swiper-tab-head class="swiper-tab" :tab-bars="tabBars" :tab-index="tabIndex" @tabtap="tabtap"></swiper-tab-head>
		<swiper class="swiper-box" :current="tabIndex" @change="tabChange">
			<swiper-item v-for="(items, index) in newsList" :key="index">
				<scroll-view scroll-y="true" class="list" @scrolltolower="loadMore(index)">
					<template v-if="items.list.length > 0">
						<!-- 图文列表 -->
						<block v-for="(item, index1) in items.list" :key="index1">
							<index-list :item="item" :index="index1" />
						</block>
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
</template>

<script>
	import IndexList from '../../components/index/index-list.vue'
	import SwiperTabHead from '../../components/index/swiper-tab-head.vue'
	import LoadMore from '../../components/common/load-more.vue'
	import Nothing from '../../components/common/no-thing.vue'

	export default {
		components: {
			IndexList,
			SwiperTabHead,
			LoadMore,
			Nothing
		},
		data() {
			return {
				tabIndex: 0,
				tabBars: [{
					name: '关注',
					id: 'guanzhu'
				}, {
					name: '推荐',
					id: 'tuijian'
				}, {
					name: '体育',
					id: 'tiyu'
				}, {
					name: '热点',
					id: 'redian'
				}, {
					name: '财经',
					id: 'caijing'
				}, {
					name: '娱乐',
					id: 'yule'
				}],
				newsList: [{
						loadText: '加载更多...',
						list: [{
								userpic: '../../static/demo/userpic/11.jpg',
								username: '昵称',
								isGuangzhu: false,
								title: '我是标题',
								type: 'img',
								titlepic: '../../static/demo/datapic/11.jpg',
								playnum: "20w", // 播放次数
								long: "2:47", // 播放时长
								infonum: {
									index: 1, // 0 代表还没有操作 1 代表 顶 2 代表踩
									dingnum: 13,
									cainum: 13
								},
								commentnum: 10,
								sharenum: 10
							},
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '昵称1',
								isGuangzhu: true,
								title: '我是标题1',
								type: 'video',
								titlepic: '../../static/demo/datapic/1.jpg',
								playnum: "20w", // 播放次数
								long: "2:47", // 播放时长
								infonum: {
									index: 2, // 0 代表还没有操作 1 代表 顶 2 代表踩
									dingnum: 12,
									cainum: 12
								},
								commentnum: 12,
								sharenum: 10
							}
						]
					},
					{
						loadText: '加载更多...',
						list: [{
								userpic: '../../static/demo/userpic/11.jpg',
								username: '昵称',
								isGuangzhu: false,
								title: '我是标题',
								type: 'img',
								titlepic: '../../static/demo/datapic/11.jpg',
								playnum: "20w", // 播放次数
								long: "2:47", // 播放时长
								infonum: {
									index: 1, // 0 代表还没有操作 1 代表 顶 2 代表踩
									dingnum: 13,
									cainum: 13
								},
								commentnum: 10,
								sharenum: 10
							},
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '昵称1',
								isGuangzhu: true,
								title: '我是标题1',
								type: 'video',
								titlepic: '../../static/demo/datapic/1.jpg',
								playnum: "20w", // 播放次数
								long: "2:47", // 播放时长
								infonum: {
									index: 2, // 0 代表还没有操作 1 代表 顶 2 代表踩
									dingnum: 12,
									cainum: 12
								},
								commentnum: 12,
								sharenum: 10
							}
						]
					},
					{
						loadText: '加载更多...',
						list: [{
								userpic: '../../static/demo/userpic/11.jpg',
								username: '昵称',
								isGuangzhu: false,
								title: '我是标题',
								type: 'img',
								titlepic: '../../static/demo/datapic/11.jpg',
								playnum: "20w", // 播放次数
								long: "2:47", // 播放时长
								infonum: {
									index: 1, // 0 代表还没有操作 1 代表 顶 2 代表踩
									dingnum: 13,
									cainum: 13
								},
								commentnum: 10,
								sharenum: 10
							},
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '昵称1',
								isGuangzhu: true,
								title: '我是标题1',
								type: 'video',
								titlepic: '../../static/demo/datapic/1.jpg',
								playnum: "20w", // 播放次数
								long: "2:47", // 播放时长
								infonum: {
									index: 2, // 0 代表还没有操作 1 代表 顶 2 代表踩
									dingnum: 12,
									cainum: 12
								},
								commentnum: 12,
								sharenum: 10
							}
						]
					},
					{
						loadText: '加载更多...',
						list: [{
								userpic: '../../static/demo/userpic/11.jpg',
								username: '昵称',
								isGuangzhu: false,
								title: '我是标题',
								type: 'img',
								titlepic: '../../static/demo/datapic/11.jpg',
								playnum: "20w", // 播放次数
								long: "2:47", // 播放时长
								infonum: {
									index: 1, // 0 代表还没有操作 1 代表 顶 2 代表踩
									dingnum: 13,
									cainum: 13
								},
								commentnum: 10,
								sharenum: 10
							},
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '昵称1',
								isGuangzhu: true,
								title: '我是标题1',
								type: 'video',
								titlepic: '../../static/demo/datapic/1.jpg',
								playnum: "20w", // 播放次数
								long: "2:47", // 播放时长
								infonum: {
									index: 2, // 0 代表还没有操作 1 代表 顶 2 代表踩
									dingnum: 12,
									cainum: 12
								},
								commentnum: 12,
								sharenum: 10
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
					if (this.newsList[index].list.length == 5) {
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

<style lang="scss" scoped>
	// 微信小程序有问题
	.list {
		display: inline;
	}
</style>


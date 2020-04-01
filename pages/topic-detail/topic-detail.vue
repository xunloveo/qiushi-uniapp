<template>
	<view>
		<topic-info :toppic-info="toppicInfo"></topic-info>
		<!-- tab切换 -->
		<swiper-tab-head :tab-bars="tabBars" :tab-index="tabIndex" :scrollViewStyle="{'border': 0}" :scrollViewItemStyle="{'width': '50%'}" @tabtap="tabtap" class="my-tab"></swiper-tab-head>
		<!-- 列表 -->
		<view class="topic-detail-list">			
			<view v-for="(item, index) in tabList" :key="index">
				<template v-if="tabIndex == index">
					<block v-for="(list, listIndex) in item.list" :key="listIndex">
						<common-list :item="list" :index="listIndex"></common-list>
					</block>
					<!-- 上拉加载 -->
					<load-more :load-text="item.loadText"></load-more>
				</template>
			</view>
		</view>
	</view>
</template>

<script>
	import TopicInfo from '../../components/topic/topic-info.vue'
	import SwiperTabHead from '../../components/index/swiper-tab-head.vue'
	import CommonList from '../../components/common/common-list.vue'
	import LoadMore from '../../components/common/load-more.vue'
	export default {
		components: {
			TopicInfo,
			SwiperTabHead,
			CommonList,
			LoadMore
		},
		data() {
			return {
				toppicInfo: {
					titlepic: '../../static/demo/topicpic/13.jpeg',
					title: '忆往事，敬余生',
					desc: '描述',
					totalnum: 1000,
					todaynum: 500
				},
				tabIndex: 0,
				tabBars: [
					{
						name: '默认',
						id: 'moren'
					},
					{
						name: '推荐',
						id: 'tuijian'
					}
				],
				tabList: [
					{
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
						]
					}
				]
			}
		},
		methods: {
			// 下拉刷新
			getData() {
				// 获取数据
				
				// 模拟
				setTimeout(() => {
					uni.stopPullDownRefresh();				
				}, 2000)
			},
			// 上拉加载
			loadMore() {
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
			tabtap(index) {
				this.tabIndex = index
			}
		},
		// 上拉加载
		onReachBottom() {
			this.loadMore()
		},
		// 下拉刷新
		onPullDownRefresh() {
			this.getData()
		}
	}
</script>


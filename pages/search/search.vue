<template>
	<view>
		<template v-if="list.length > 0">
			<block v-for="(item, index) in list" :key="index">
				<index-list :item="item" :index="index"></index-list>
			</block>
			<!-- 上拉加载 -->
			<load-more :load-text="loadText"></load-more>
		</template>
		<template v-else-if="isSearch && list.length == 0">
			<nothing></nothing>
		</template>

	</view>
</template>

<script>
	import IndexList from '../../components/index/index-list.vue'
	import LoadMore from '../../components/common/load-more.vue'
	import Nothing from '../../components/common/no-thing.vue'
	export default {
		components: {
			IndexList,
			LoadMore,
			Nothing
		},
		data() {
			return {
				isSearch: false,
				loadText: '加载更多...',
				list: [],
				searchText: ''
			}
		},
		// 监听原生标题栏按钮点击事件
		onNavigationBarButtonTap(e) {
			// 点击了取消 返回上一级
			if (e.index === 0) {
				uni.navigateBack({
					delta: 1
				})
			}
		},
		// 监听原生标题栏搜索输入框输入内容变化事件
		onNavigationBarSearchInputChanged(e) {			
			this.searchText = e.text
		},
		// 监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发
		onNavigationBarSearchInputConfirmed(e) {
			if (e.text) {
				this.getData()
			}			
		},
		// 上拉触底
		onReachBottom() {
			this.loadMore()
		},
		// 监听下拉刷新
		onPullDownRefresh() {
			this.getData()
			uni.stopPullDownRefresh()
		},
		methods: {
			// 搜索时间
			getData() {
				// 请求服务器数据
				uni.showLoading()
				setTimeout(() => {
					let arr = [{
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
						},
						{
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
						}
					]
					this.isSearch = true
					this.list = arr
					uni.hideLoading()
				}, 2000)
			},
			// 上拉加载
			loadMore() {
				console.log(this.loadText)
				if (this.loadText != '加载更多...') return
				this.loadText = '加载中...'
				setTimeout(() => {
					let obj = this.list[0]
					this.list.push(obj)
					if (this.list.length == 5) {
						this.loadText = '已经触底了...'
						return
					}
					this.loadText = '加载更多...'

				}, 1000)

			},
		}
	}
</script>

<style>

</style>

<template>
	<view class="paper-container">
		<!-- 操作菜单 -->
		<paper-popup :show="show" @hide="hidePopup" @add-friend="addFreiend" @clear-cache="clearCache"></paper-popup>
		<block v-for="(item, index) in list" :key="index">
			<paper-list :item="item" :index="index"></paper-list>
		</block>
		<!-- 上拉加载 -->
		<load-more :load-text="loadText"></load-more>
	</view>
</template>

<script>
	import PaperPopup from '../../components/paper/paper-popup.vue'
	import PaperList from '../../components/paper/paper-list.vue'
	import LoadMore from '../../components/common/load-more.vue'
	export default {
		components: {
			PaperPopup,
			PaperList,
			LoadMore
		},
		data() {
			return {
				show: false,
				loadText: '加载更多...',
				list: [{
						userpic: '../../static/demo/userpic/1.jpg',
						username: '昵称',
						time: '10:21',
						data: '信息',
						noreadnum: 10
					},
					{
						userpic: '../../static/demo/userpic/2.jpg',
						username: '昵称',
						time: '10:21',
						data: '信息',
						noreadnum: 0
					},
					{
						userpic: '../../static/demo/userpic/3.jpg',
						username: '昵称',
						time: '10:21',
						data: '信息',
						noreadnum: 0
					},
					{
						userpic: '../../static/demo/userpic/1.jpg',
						username: '昵称',
						time: '10:21',
						data: '信息',
						noreadnum: 10
					},
					{
						userpic: '../../static/demo/userpic/2.jpg',
						username: '昵称',
						time: '10:21',
						data: '信息',
						noreadnum: 0
					},
					{
						userpic: '../../static/demo/userpic/3.jpg',
						username: '昵称',
						time: '10:21',
						data: '信息',
						noreadnum: 0
					},
					{
						userpic: '../../static/demo/userpic/1.jpg',
						username: '昵称',
						time: '10:21',
						data: '信息',
						noreadnum: 10
					},
					{
						userpic: '../../static/demo/userpic/2.jpg',
						username: '昵称',
						time: '10:21',
						data: '信息',
						noreadnum: 0
					},
					{
						userpic: '../../static/demo/userpic/3.jpg',
						username: '昵称',
						time: '10:21',
						data: '信息',
						noreadnum: 0
					}
				]
			}
		},
		methods: {
			getData() {
				setTimeout(() => {
					// 获取数据
					let arr = [{
							userpic: '../../static/demo/userpic/11.jpg',
							username: '昵称1',
							time: '11:21',
							data: '信息',
							noreadnum: 10
						},
						{
							userpic: '../../static/demo/userpic/12.jpg',
							username: '昵称2',
							time: '11:21',
							data: '信息',
							noreadnum: 0
						},
						{
							userpic: '../../static/demo/userpic/13.jpg',
							username: '昵称3',
							time: '11:21',
							data: '信息',
							noreadnum: 0
						},
						{
							userpic: '../../static/demo/userpic/11.jpg',
							username: '昵称1',
							time: '11:21',
							data: '信息',
							noreadnum: 10
						},
						{
							userpic: '../../static/demo/userpic/12.jpg',
							username: '昵称2',
							time: '11:21',
							data: '信息',
							noreadnum: 0
						},
						{
							userpic: '../../static/demo/userpic/13.jpg',
							username: '昵称3',
							time: '11:21',
							data: '信息',
							noreadnum: 0
						},
						{
							userpic: '../../static/demo/userpic/11.jpg',
							username: '昵称1',
							time: '11:21',
							data: '信息',
							noreadnum: 10
						},
						{
							userpic: '../../static/demo/userpic/12.jpg',
							username: '昵称2',
							time: '11:21',
							data: '信息',
							noreadnum: 0
						},
						{
							userpic: '../../static/demo/userpic/13.jpg',
							username: '昵称3',
							time: '11:21',
							data: '信息',
							noreadnum: 0
						}
					]
					this.list = arr
					uni.stopPullDownRefresh();
				}, 2000)
			},
			// 上拉加载
			LoadMore() {
				if (this.loadText != '加载更多...') return
				this.loadText = '加载中...'
				setTimeout(() => {
					let obj = this.list[Math.floor(Math.random() * 4)]
					this.list.push(obj)
					if (this.list.length == 18) {
						this.loadText = '已经触底了...'
						return
					}
					this.loadText = '加载更多...'
				}, 1000)
			},
			// 添加糗友
			addFreiend() {
				this.hidePopup()
			},
			// 清除缓存
			clearCache() {
				this.hidePopup()
			},
			// 隐藏
			hidePopup() {
				this.show = false
			},
			// 显示
			showPopup() {
				this.show = true
			}
		},
		// 监听下拉刷新
		onPullDownRefresh() {
			this.getData()
		},
		// 上拉加载
		onReachBottom() {
			this.LoadMore()
		},
		// 监听导航按钮点击事件
		onNavigationBarButtonTap(e) {
			switch (e.index) {
				case 0: // 左边按钮
					uni.navigateTo({
						url: '../user-list/user-list'
					});
					this.hidePopup()
					break;
				case 1: // 右边按钮
					this.showPopup()
					break;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.paper-container {
		padding: 0 20rpx;
	}
</style>

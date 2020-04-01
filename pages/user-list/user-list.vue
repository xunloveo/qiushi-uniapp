<template>
	<view class="user-list-container">
		<!-- tab栏 -->
		<swiper-tab-head :tab-bars="tabBars" :tab-index="tabIndex" :scrollViewStyle="{'border': 0}" :scrollViewItemStyle="{'width': '33%'}"
		 @tabtap="tabtap"></swiper-tab-head>
		<!-- 列表组件 -->
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{'height': swiperHeight + 'px'}" :current="tabIndex" @change="tabChange">
				<swiper-item v-for="(items, index) in userList" :key="index">
					<scroll-view scroll-y="true" class="list" @scrolltolower="loadMore(index)">
						<template v-if="items.list.length > 0">
							<!-- 图文列表 -->
							<block v-for="(item, index1) in items.list" :key="index1">
								<user-list :item="item" :index="index1"></user-list>
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
				
	</view>
</template>

<script>
	import SwiperTabHead from '../../components/index/swiper-tab-head.vue'
	import UserList from '../../components/user-list/user-list.vue'
	import LoadMore from '../../components/common/load-more.vue'
	import Nothing from '../../components/common/no-thing.vue'
	export default {
		components: {
			SwiperTabHead,
			UserList,
			LoadMore,
			Nothing
		},
		data() {
			return {
				swiperHeight: 500,
				tabIndex: 0,
				tabBars: [{
						name: '互关',
						id: 'huguan',
						num: 10
					},
					{
						name: '关注',
						id: 'guanzhu',
						num: 20
					},
					{
						name: '粉丝',
						id: 'fensi',
						num: 30
					}
				],
				userList: [
					{
						loadText: '加载更多...',
						list: [
							{
								userpic: '../../static/demo/userpic/1.jpg',
								username: '昵称',
								age: 20,
								sex: 1,
								isguangzhu: true
							},
							{
								userpic: '../../static/demo/userpic/2.jpg',
								username: '昵称',
								age: 20,
								sex: 1,
								isguangzhu: false
							},
							{
								userpic: '../../static/demo/userpic/1.jpg',
								username: '昵称',
								age: 20,
								sex: 1,
								isguangzhu: true
							},
							{
								userpic: '../../static/demo/userpic/2.jpg',
								username: '昵称',
								age: 20,
								sex: 1,
								isguangzhu: false
							},
							{
								userpic: '../../static/demo/userpic/1.jpg',
								username: '昵称',
								age: 20,
								sex: 1,
								isguangzhu: true
							},
							{
								userpic: '../../static/demo/userpic/2.jpg',
								username: '昵称',
								age: 20,
								sex: 1,
								isguangzhu: false
							},
							{
								userpic: '../../static/demo/userpic/1.jpg',
								username: '昵称',
								age: 20,
								sex: 1,
								isguangzhu: true
							},
							{
								userpic: '../../static/demo/userpic/2.jpg',
								username: '昵称',
								age: 20,
								sex: 1,
								isguangzhu: false
							},
							{
								userpic: '../../static/demo/userpic/1.jpg',
								username: '昵称',
								age: 20,
								sex: 1,
								isguangzhu: true
							},
							{
								userpic: '../../static/demo/userpic/2.jpg',
								username: '昵称',
								age: 20,
								sex: 1,
								isguangzhu: false
							}
						]
					},
					{
						loadText: '加载更多...',
						list: [
							{
								userpic: '../../static/demo/userpic/1.jpg',
								username: '昵称',
								age: 20,
								sex: 1,
								isguangzhu: true
							},
							{
								userpic: '../../static/demo/userpic/2.jpg',
								username: '昵称',
								age: 20,
								sex: 1,
								isguangzhu: false
							}
						]
					},
					{
						loadText: '加载更多...',
						list: [
							{
								userpic: '../../static/demo/userpic/1.jpg',
								username: '昵称',
								age: 20,
								sex: 1,
								isguangzhu: true
							},
							{
								userpic: '../../static/demo/userpic/2.jpg',
								username: '昵称',
								age: 20,
								sex: 1,
								isguangzhu: false
							}
						]
					}
				]				
			}
		},
		methods: {
			// 上拉加载
			loadMore(index) {
				if (this.userList[index].loadText != '加载更多...') return
				this.userList[index].loadText = '加载中...'
				setTimeout(() => {
					let obj = this.userList[index].list[0]
					this.userList[index].list.push(obj)
					if (this.userList[index].list.length == 20) {
						this.userList[index].loadText = '已经触底了...'
						return
					}
					this.userList[index].loadText = '加载更多...'
			
				}, 1000)
			
			},
			tabtap(index) {
				this.tabIndex = index
			},
			tabChange(e) {
				this.tabIndex = e.target.current || e.detail.current
			}	
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res) => {
					this.swiperHeight = res.windowHeight - uni.upx2px(100)
				}
			})
		},
		// 监听导航事件
		onNavigationBarButtonTap(e) {
			if (e.index === 0) {
				uni.navigateBack({
					delta: 1
				});
			}
		}
	}
</script>

<style lang="scss" scoped>
	.user-list-container {
		padding: 0 20rpx;
	}	
</style>

<template>
	<view>
		<!-- 聊天列表 -->
		<scroll-view id="scrollview" scroll-y :scroll-top="scrollTop" :scroll-with-animation="true">
			<view class="test">
				<block v-for="(item, index) in list" :key="index">
					<user-chat-list class="user-chat-item" :item="item" :index="index"></user-chat-list>
				</block>
			</view>
		</scroll-view>
		<!-- 输入框 -->
		<user-chat-bottom @send="send"></user-chat-bottom>
	</view>
</template>

<script>
	import UserChatBottom from '../../components/user-chat/user-chat-bottom.vue'
	import UserChatList from '../../components/user-chat/user-chat-list.vue'
	import Time from '../../common/time.js'
	export default {
		components: {
			UserChatBottom,
			UserChatList
		},
		data() {
			return {
				list: [],
				style: {
					contentH: 0,
					itemH: 0
				},
				scrollTop: 0
			}
		},
		onReady() {
			this.pageToBottom()
		},
		onLoad() {
			this.getData()
			this.initData()
		},
		methods: {
			// 初始化参数
			initData() {
				try {
					const res = uni.getSystemInfoSync();
					/* const data = ['iPhone11', 'iPhoneX']
					if (data.indexOf(res.model) !== -1) {
						// 计算安全区域(目前不知道原因)
						this.style.contentH = res.windowHeight - uni.upx2px(121) 
					} else {
						this.style.contentH = res.windowHeight - uni.upx2px(121);
					} */
					this.style.contentH = res.windowHeight - uni.upx2px(121);
				} catch (e) {
					//TODO handle the exception
				}
			},
			pageToBottom() {
				let q = uni.createSelectorQuery();
				q.select('#scrollview').boundingClientRect();
				q.selectAll('.user-chat-item').boundingClientRect();

				q.exec((res) => {
					res[1].forEach((ret) => {
						this.style.itemH += ret.height;
					});

					if (this.style.itemH > this.style.contentH) {
						this.scrollTop = this.style.itemH;
					}

				})

			},
			//获取聊天数据
			getData() {
				let arr = [{
						isme: false,
						userpic: '../../static/demo/userpic/1.jpg',
						type: 'text',
						data: '聊天随你聊聊天随你聊聊天随你聊聊天随你聊聊天随你聊聊天随你聊聊天随你聊聊天随你聊',
						time: '1584687149',
					},
					{
						isme: true,
						userpic: '../../static/demo/userpic/2.jpg',
						type: 'img',
						data: '../../static/demo/3.jpg',
						time: '1584688350',
					},
					{
						isme: false,
						userpic: '../../static/demo/userpic/1.jpg',
						type: 'text',
						data: '聊天随你聊聊天随你聊聊天随你聊聊天随你聊聊天随你聊聊天随你聊聊天随你聊聊天随你聊',
						time: '1584687149',
					},
					{
						isme: true,
						userpic: '../../static/demo/userpic/2.jpg',
						type: 'img',
						data: '../../static/demo/3.jpg',
						time: '1584688350',
					},
					{
						isme: false,
						userpic: '../../static/demo/userpic/1.jpg',
						type: 'text',
						data: '聊天随你聊聊天随你聊聊天随你聊聊天随你聊聊天随你聊聊天随你聊聊天随你聊聊天随你聊',
						time: '1584687149',
					},
					{
						isme: true,
						userpic: '../../static/demo/userpic/2.jpg',
						type: 'img',
						data: '../../static/demo/3.jpg',
						time: '1584688350',
					}
				]
				arr.map((item, index) => {
					item.gstime = Time.gettime.getChatTime(item.time, index > 0 ? arr[index - 1].time : 0)
				})
				this.list = arr
			},
			// 发送信息
			send(text) {
				// 构建数据
				let now = +new Date()
				let obj = {
					isme: true,
					userpic: '../../static/demo/userpic/1.jpg',
					type: 'text',
					data: text,
					time: now,
					gstime: Time.gettime.getChatTime(now, this.list[this.list.length - 1].time)
				}
				this.list.push(obj)
				this.pageToBottom()
			}
		}
	}
</script>

<style lang="scss" scoped>	
	#scrollview {
		box-sizing: border-box;
		height: 100vh;
		padding-bottom: 121rpx;
	}
</style>

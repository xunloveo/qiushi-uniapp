<template>
	<view class="detail-container animated fadeIn">
		<detail-info :item="detailInfo"></detail-info>
		<!-- 评论区 -->
		<view class="u-comment-title">最新评论 1</view>
		<view class="uni-comment u-comment">
			<block v-for="(item, index) in comment.list" :key="item.id">
				<comment-list :item="item" :index="index"></comment-list>
			</block>
		</view>

		<!-- 占位符 -->
		<view style="height: 120rpx;"></view>
		<!-- 输入框 -->
		<user-chat-bottom @send="send"></user-chat-bottom>

		<more-share :show="shareShow" @toggle="toggleShareShow" :provider-list="providerList" @share="share"></more-share>
	</view>
</template>

<script>
	import DetailInfo from '../../components/detail/detail-info.vue'
	import CommentList from '../../components/detail/comment-list.vue'
	import UserChatBottom from '../../components/user-chat/user-chat-bottom.vue'
	import MoreShare from '../../components/common/more-share.vue'
	import Time from '../../common/time.js'
	export default {
		components: {
			DetailInfo,
			CommentList,
			UserChatBottom,
			MoreShare
		},
		data() {
			return {
				title: 'share',
				shareText: 'uni-app可以同时发布成原生App、小程序、H5，邀请你一起体验！',
				href: "https://uniapp.dcloud.io",
				image: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png',
				shareType: 1, // 1 文字 2, 0 图文 5小程序 
				providerList: [],
				shareShow: false,
				comment: {
					count: 20,
					list: []
				},
				detailInfo: {
					userpic: "../../static/demo/userpic/12.jpg",
					username: "哈哈",
					sex: 0, //0 男 1 女
					age: 25,
					isguanzhu: false,
					title: "我是标题",
					titlepic: "../../static/demo/datapic/12.jpg",
					morepic: ["../../static/demo/datapic/12.jpg", "../../static/demo/datapic/13.jpg",
						"../../static/demo/datapic/14.jpg"
					],
					video: false,
					share: false,
					path: "深圳 龙岗",
					sharenum: 20,
					commentnum: 30,
					goodnum: 20
				}
			}
		},
		methods: {
			async share(e) {
				console.log('分享通道:' + e.id + '； 分享类型:' + this.shareType);

				if (!this.shareText && (this.shareType === 1 || this.shareType === 0)) {
					uni.showModal({
						content: '分享内容不能为空',
						showCancel: false
					})
					return;
				}

				if (!this.image && (this.shareType === 2 || this.shareType === 0)) {
					uni.showModal({
						content: '分享图片不能为空',
						showCancel: false
					})
					return;
				}

				let shareOPtions = {
					provider: e.id,
					scene: e.type && e.type === 'WXSenceTimeline' ? 'WXSenceTimeline' : 'WXSceneSession', //WXSceneSession”分享到聊天界面，“WXSenceTimeline”分享到朋友圈，“WXSceneFavorite”分享到微信收藏     
					type: this.shareType,
					success: (e) => {
						console.log('success', e);
						uni.showModal({
							content: '分享成功',
							showCancel: false
						})
					},
					fail: (e) => {
						console.log('fail', e)
						uni.showModal({
							content: e.errMsg,
							showCancel: false
						})
					},
					complete: function() {
						console.log('分享操作结束!')
					}
				}

				switch (this.shareType) {
					case 0:
						shareOPtions.summary = this.shareText;
						shareOPtions.imageUrl = this.image;
						shareOPtions.title = '欢迎体验uniapp';
						shareOPtions.href = 'https://uniapp.dcloud.io';
						break;
					case 1:
						shareOPtions.summary = this.shareText;
						break;
					case 2:
						shareOPtions.imageUrl = this.image;
						break;
					case 5:
						shareOPtions.imageUrl = this.image ? this.image :
							'https://img-cdn-qiniu.dcloud.net.cn/uniapp/app/share-logo@3.png'
						shareOPtions.title = '欢迎体验uniapp';
						shareOPtions.miniProgram = {
							id: 'gh_33446d7f7a26',
							path: '/pages/tabBar/component/component',
							webUrl: 'https://uniapp.dcloud.io',
							type: 0
						};
						break;
					default:
						break;
				}

				if (shareOPtions.type === 0 && plus.os.name === 'iOS') { //如果是图文分享，且是ios平台，则压缩图片 
					shareOPtions.imageUrl = await this.compress();
				}
				if (shareOPtions.type === 1 && shareOPtions.provider === 'qq') { //如果是分享文字到qq，则必须加上href和title
					shareOPtions.href = 'https://uniapp.dcloud.io';
					shareOPtions.title = '欢迎体验uniapp';
				}
				uni.share(shareOPtions);
			},
			compress() { //压缩图片 图文分享要求分享图片大小不能超过20Kb
				console.log('开始压缩');
				let img = this.image;
				return new Promise((res) => {
					var localPath = plus.io.convertAbsoluteFileSystem(img.replace('file://', ''));
					console.log('after' + localPath);
					// 压缩size
					plus.io.resolveLocalFileSystemURL(localPath, (entry) => {
						entry.file((file) => { // 可通过entry对象操作图片 
							console.log('getFile:' + JSON.stringify(file));
							if (file.size > 20480) { // 压缩后size 大于20Kb
								plus.zip.compressImage({
									src: img,
									dst: img.replace('.jpg', '2222.jpg').replace('.JPG', '2222.JPG'),
									width: '10%',
									height: '10%',
									quality: 1,
									overwrite: true
								}, (event) => {
									console.log('success zip****' + event.size);
									let newImg = img.replace('.jpg', '2222.jpg').replace('.JPG', '2222.JPG');
									res(newImg);
								}, function(error) {
									uni.showModal({
										content: '分享图片太大,需要请重新选择图片!',
										showCancel: false
									})
								});
							}
						});
					}, (e) => {
						console.log('Resolve file URL failed: ' + e.message);
						uni.showModal({
							content: '分享图片太大,需要请重新选择图片!',
							showCancel: false
						})
					});
				})
			},

			// 获取数据
			getData() {
				let arr = [{
						id: 1,
						fid: 0,
						userpic: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png',
						username: '小猫咪',
						time: +new Date(),
						data: '支持国产，支持DCloud!'
					},
					{
						id: 2,
						fid: 1,
						userpic: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png',
						username: '小猫咪',
						time: +new Date(),
						data: '支持国产，支持DCloud!'
					},
					{
						id: 3,
						fid: 1,
						userpic: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png',
						username: '小猫咪',
						time: +new Date(),
						data: '支持国产，支持DCloud!'
					},
					{
						id: 4,
						fid: 0,
						userpic: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png',
						username: '小猫咪',
						time: +new Date(),
						data: '支持国产，支持DCloud!'
					}
				]
				arr.map(item => {
					item.time = Time.gettime.gettime(item.time)
				})
				this.comment.list = arr
			},
			// 初始化数据
			initData(data) {
				uni.setNavigationBarTitle({
					title: data.title
				})
			},
			// 发送信息
			send(text) {
				// 构建数据
				let obj = {
					id: 1,
					fid: 0,
					userpic: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png',
					username: '小猫咪',
					time: +new Date(),
					data: text
				}
				obj.time = Time.gettime.gettime(obj.time)
				this.comment.list.push(obj)
			},
			toggleShareShow(show) {
				this.shareShow = show
			}
		},
		onLoad(e) {
			if (e.detailData) {
				this.initData(JSON.parse(e.detailData))
			}
			this.getData()
			uni.getProvider({
				service: 'share',
				success: (e) => {
					console.log('success', e);
					let data = []
					for (let i = 0; i < e.provider.length; i++) {
						switch (e.provider[i]) {
							case 'weixin':
								data.push({
									name: '微信好友',
									id: 'weixin',
									icon: 'weixin',
									class: 'wx',
									sort: 0
								})
								data.push({
									name: '朋友圈',
									id: 'weixin',
									icon: 'weixin',
									class: 'pyq',
									type: 'WXSenceTimeline',
									sort: 1
								})
								break;
							case 'sinaweibo':
								data.push({
									name: '新浪微博',
									icon: 'xinlangweibo',
									class: 'wb',
									id: 'sinaweibo',
									sort: 2
								})
								break;
							case 'qq':
								data.push({
									name: 'QQ好友',
									id: 'qq',
									icon: 'qq',
									class: 'qq',
									sort: 3
								})
								break;
							default:
								break;
						}
					}
					this.providerList = data.sort((x, y) => {
						return x.sort - y.sort
					});
				},
				fail: (e) => {
					console.log('获取分享通道失败', e);
					uni.showModal({
						content: '获取分享通道失败',
						showCancel: false
					})
				}
			});

		},
		// 监听导航栏事件
		onNavigationBarButtonTap(e) {
			if (e.index === 0) {
				this.shareShow = true
			}
		}

	}
</script>

<style lang="scss">
	.detail-container {
		.common-list {
			border-bottom: 1rpx solid #eeeeee;

			.common-list-right {
				border-bottom: 0 !important;
			}
		}

		.common-list-right-time {
			padding: 15rpx 0;
			color: #cccccc;
			font-size: 25rpx;
		}

		.u-comment-title {
			padding: 20rpx;
			font-size: 30rpx;
			font-weight: bold;
		}

	}
</style>

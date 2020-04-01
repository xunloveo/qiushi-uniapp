<template>
	<view>
		<!-- 自定义导航栏 -->
		<uni-nav-bar :statusBar="true" left-icon="back" right-text="发布" @click-left="back" @click-right="submit">
			<view class="u-f u-f-center" style="margin: 0 auto;" @tap="changeLook">
				<text>{{sercet}}</text>
				<view class="icon iconfont icon-xialazhankai"></view>
			</view>
		</uni-nav-bar>
		<!-- 多行输入框 -->
		<view class="uni-textarea">
			<textarea v-model="text" placeholder="说一句话吧" />
			</view>		
		<!-- 上传多图 -->
		<upload-image  @upload="upload"></upload-image>
		<!-- 弹出公告 -->
		<uni-popup  ref="popup" type="center" :maskClick="false" :custom="true" @change="change" show>
			<view class="gonggao">
				<view class="u-f-center">
					<image src="../../static/common/addinput.png" mode="widthFix"></image>
				</view>	
				<view class="tal">1. 涉及黄色，政治，广告及骚扰信息</view>
				<view class="tal">2. 涉及人身攻击</view>
				<view class="tal">3. 留联系方式，透露他人隐私</view>
				<view class="tal">一经核实将被封禁，情节严重者永久封禁</view>
				<button type="primary" class="btn" @click="close">朕知道了</button>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	import uniNavBar from '../../components/uni-nav-bar/uni-nav-bar.vue'
	import UploadImage from '../../components/common/upload-image.vue'
	import uniPopup from '../../components/uni-popup/uni-popup.vue'
	
	let changLookText = ['所有人可见', '仅自己可见']	
	export default {
		components: {
			uniNavBar,
			UploadImage,
			uniPopup
		},
		data() {
			return {				
				sercet: '所有人可见',
				text: '',
				imageList: [],
				isSave: false // 是否弹出了保存草稿
			}
		},
		// 监听返回行为
		onBackPress() {
			if(this.text == '' && this.imageList.length == 0) return
			if(!this.isSave) {
				this.save()
				return true
			}			
		},
		onLoad() {
			// 在ios上 需要这么解决(因为默认给show不显示)
			setTimeout(() => {
				this.open()
			}, 0)			
		},
		methods: {
			// 返回
			back() {
				uni.navigateBack()
			},
			// 发布
			submit() {
				console.log('发布')
			},
			// 隐私
			changeLook() {				
				uni.showActionSheet({
					itemList: changLookText,
					success: (res) => {
						this.sercet = changLookText[res.tapIndex]
					}
				})
			},
			upload(arr) {
				this.imageList = arr
				console.log(this.imageList)
			},
			change(e) {
				console.log('e', e)
			},
			// 打开弹窗
			open(){
			    this.$refs.popup.open()
			},
			// 关闭弹窗
			close() {
				this.$refs.popup.close()
			},
			// 保存草稿逻辑
			save() {
				uni.showModal({
					content: '是否需要保存为草稿？',
					cancelText: '不保存',
					confirmText: '保存',
					success: res => {					
						if(res.confirm) { // 保存
							
						} else { // 不保存
						
						}
						this.isSave = true
						uni.navigateBack({
							delta: 1
						})						
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
.uni-textarea {
	border: 1px solid #EEEEEE;
}

.gonggao {	
	padding: 20rpx;
	background: #FFFFFF;
	
	image {
		width: 75%;
		margin-bottom: 20rpx;;
	}
	
	.btn {
		margin-top: 20rpx;
		color: #171606;
		background: #FFE934;
	}
}
</style>

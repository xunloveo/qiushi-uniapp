<template>
	<view class="setting-container">
		<view class="user-set-userinfo-list u-f u-f-ac u-f-jcsb">
			<view class="title">头像</view>
			<view class="u-f u-f-ac" @tap="changeImg">
				<image :src="userpic" mode="aspectFill" lazy-load></image>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list u-f u-f-ac u-f-jcsb">
			<view class="title">昵称</view>
			<view class="u-f u-f-ac">
				<input type="text" v-model="username" class="userinfo-input">
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list u-f u-f-ac u-f-jcsb">
			<view class="title">性别</view>
			<view class="u-f u-f-ac" @tap="changeOne('sex')">
				<view>{{sex}}</view>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list u-f u-f-ac u-f-jcsb">
			<view class="title">生日</view>
			<picker mode="date" :value="birthday" :start="startDate" :end="endDate" @change="bindDateChange">
				<view class="u-f u-f-ac">
					<view>{{birthday}}</view>
					<view class="icon iconfont icon-bianji1"></view>
				</view>
			</picker>
		</view>
		<view class="user-set-userinfo-list u-f u-f-ac u-f-jcsb">
			<view class="title">情感</view>
			<view class="u-f u-f-ac" @tap="changeOne('qg')">
				<view>{{qg}}</view>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list u-f u-f-ac u-f-jcsb">
			<view class="title">职业</view>
			<view class="u-f u-f-ac" @tap="changeOne('job')">
				<view>{{job}}</view>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>
		<view class="user-set-userinfo-list u-f u-f-ac u-f-jcsb">
			<view class="title">家乡</view>
			<view class="u-f u-f-ac" @tap="showMulLinkageThreePicker">
				<view>{{pickerText}}</view>
				<view class="icon iconfont icon-bianji1"></view>
			</view>
		</view>

		<mpvue-city-picker themeColor="#007AFF" ref="mpvueCityPicker" :pickerValueDefault="cityPickerValueDefault" @onConfirm="onConfirm"></mpvue-city-picker>

		<button type="primary" class="user-setting-btn" @tap="complete">完成</button>
	</view>
</template>

<script>
	let sexOptions = ['不限', '男', '女']
	let qgOptions = ['秘密', '未婚', '已婚']
	let jobOptions = ['IT', '老师', '厨师']
	let objOptions = {
		'sex': sexOptions,
		'qg': qgOptions,
		'job': jobOptions
	}
	import mpvueCityPicker from '../../components/mpvue-citypicker/mpvueCityPicker.vue'
	export default {
		components: {
			mpvueCityPicker
		},
		data() {
			return {
				userpic: '../../static/demo/userpic/11.jpg',
				username: '哈哈',
				sex: '男',
				qg: '未婚',
				job: 'IT',
				birthday: '1996-04-01',
				cityPickerValueDefault: [0, 0, 1],
				pickerText: '江西省-南昌市-东湖区'
			}
		},
		computed: {
			startDate() {
				return this.getDate('start');
			},
			endDate() {
				return this.getDate('end');
			}
		},
		onBackPress() {
			if (this.$refs.mpvuePicker.showPicker) {
				this.$refs.mpvuePicker.pickerCancel();
				return true;
			}
			if (this.$refs.mpvueCityPicker.showPicker) {
				this.$refs.mpvueCityPicker.pickerCancel();
				return true;
			}
		},
		onUnload() {
			if (this.$refs.mpvuePicker.showPicker) {
				this.$refs.mpvuePicker.pickerCancel()
			}
			if (this.$refs.mpvueCityPicker.showPicker) {
				this.$refs.mpvueCityPicker.pickerCancel()
			}
		},
		methods: {
			// 三级联动选择
			showMulLinkageThreePicker() {
				this.$refs.mpvueCityPicker.show()
			},
			onConfirm(e) {
				this.pickerText = e.label
			},
			// 修改生日
			bindDateChange: function(e) {
				this.birthday = e.target.value
			},
			getDate(type) {
				const date = new Date();
				let year = date.getFullYear();
				let month = date.getMonth() + 1;
				let day = date.getDate();

				if (type === 'start') {
					year = year - 60;
				} else if (type === 'end') {
					year = year + 2;
				}
				month = month > 9 ? month : '0' + month;;
				day = day > 9 ? day : '0' + day;
				return `${year}-${month}-${day}`;
			},
			// 修改头像
			changeImg() {
				uni.chooseImage({
					count: 1,
					sizeType: ['compressed'],
					success: (res) => {
						this.userpic = res.tempFilePaths[0]
					}
				})
			},
			// 性别 职业 情感 共同操作
			changeOne(val) {
				uni.showActionSheet({
					itemList: objOptions[val],
					success: (res) => {
						this[val] = objOptions[val][res.tapIndex]
					}
				})
			},
			complete() {

			}
		}
	}
</script>

<style lang="scss" scoped>
	@import "../../common/form.scss";

	.user-set-userinfo-list {
		padding: 20rpx;
		border-bottom: 1rpx solid #f4f4f4;

		.title {
			font-size: 32rpx;
			font-weight: bold;
			color: #9b9b9b;
		}

		image {
			width: 80rpx;
			height: 80rpx;
			border-radius: 100%;
		}

		.icon {
			margin-left: 20rpx;
			color: #9b9b9b;
		}

		.userinfo-input {
			text-align: right;
		}
	}
</style>

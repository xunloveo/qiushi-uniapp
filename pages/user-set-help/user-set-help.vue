<template>
	<view >
		<uni-collapse :accordion="true">
			<uni-collapse-item v-for="item in accordion" :key="item.id" :title="item.title" :show-animation="item.animation">
				<view class="content">{{ item.content }}</view>
			</uni-collapse-item>
		</uni-collapse>
		<button type="primary" class="user-setting-btn">意见反馈</button>
	</view>
</template>

<script>
	import uniCollapse from '@/components/uni-collapse/uni-collapse.vue'
	import uniCollapseItem from '@/components/uni-collapse-item/uni-collapse-item.vue'
	export default {
		components: {
			uniCollapse,
			uniCollapseItem
		},
		data() {
			return {
				accordion: [{
						id: 0,
						title: '客服什么时候在线？',
						content: '亲爱的仿糗友，客服的工作时间为：周一至周六10:00-12:00,14:00-19:00，非工作时间的咨询反馈会自动转为留言，客服上班后会第一时间回复哦~',
						animation: true
					},
					{
						id: 1,
						title: '忘记账号/昵称/密码怎么办？',
						content: '手风琴效果',
						animation: true
					},
					{
						id: 2,
						title: '怎么搜索/查找、关注/取关用户？',
						content: '手风琴效果',
						animation: true
					}
				],
			}
		},
		methods: {
			
		}
	}
</script>

<style lang="scss" scoped>
@import  "../../common/form.scss";

.content {
	padding: 20rpx 30rpx;
	background: #ffffff;
}
</style>


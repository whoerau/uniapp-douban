<template>
	<view>
		<!-- 基础用法 -->
		<uni-swipe-action>
			<uni-swipe-action-item :options="options" @click="onClick" @change="change">
				<view class='cont'>每一item项212122</view>
			</uni-swipe-action-item>
			<uni-swipe-action-item :options="options" @click="onClick" @change="change">
				<view class='cont'>每一item项212122</view>
			</uni-swipe-action-item>
			<uni-swipe-action-item :options="options" @click="onClick" @change="change">
				<view class='cont'>每一item项212122</view>
			</uni-swipe-action-item>
		</uni-swipe-action>



	</view>
</template>

<script>
	import uniSwipeAction from '@/components/uni-swipe-action/uni-swipe-action.vue'
	import uniSwipeActionItem from '@/components/uni-swipe-action-item/uni-swipe-action-item.vue'
	export default {
		components: {
			uniSwipeAction,
			uniSwipeActionItem
		},
		data: () => ({
			options: [ {
				text: '删除	',
				style: {
					backgroundColor: '#FF4645'
				}
			}]
		}),
		methods: {
			onClick(e) {
				console.log('当前点击的是第' + e.index + '个按钮，点击内容是' + e.content.text)
				uni.showModal({
				    title: '提示',
				    content: '此操作不可逆，是否确认删除',
				    success: (res)=> {
				        if (res.confirm) {
				            console.log('用户点击确定');
				        } else if (res.cancel) {
				            console.log('用户点击取消');
				        }
				    }
				});
			},
			change(open) {
				// console.log('当前开启状态：' + open)
			}
		}
	}
</script>

<style lang="scss" scoped>
.cont{
	// background-color: pink;
}
</style>

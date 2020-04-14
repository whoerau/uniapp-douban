<template>
	<view>
		<!-- 基础用法 -->
		<!-- <uni-swipe-action>
			<uni-swipe-action-item :options="options" @click="onClick" @change="change">
				<view class='cont'>每一item项212122</view>
			</uni-swipe-action-item>
			<uni-swipe-action-item :options="options" @click="onClick" @change="change">
				<view class='cont'>每一item项212122</view>
			</uni-swipe-action-item>
			<uni-swipe-action-item :options="options" @click="onClick" @change="change">
				<view class='cont'>每一item项212122</view>
			</uni-swipe-action-item>
		</uni-swipe-action> -->


		<!-- <text>首页</text>
		<view>
			<me-select ref="meSelect" @change="change" @finish="finish" @itemClick="itemClick" :datalist="dataList" :options="options">
				<view slot-scope="slot" class="item">
					<view>{{slot.slotScope.item.id}}</view>
				</view>
			</me-select>
			<button @click="changeModel">编辑/取消</button>
			<button @click="getSelectAll">获取所有选中的列表</button>
		</view> -->

		<view>



			<view class="uni-list">
				<checkbox-group @change="checkboxChange">
					<label class="uni-list-cell uni-list-cell-pd" v-for="item in items" :key="item.value">
						<view v->
							<checkbox :value="item.value" :checked="item.checked" />
						</view>
						<view>{{item.name}}</view>
					</label>
				</checkbox-group>
			</view>
			<view class="">
				<button type="default" @click="handleAllChoose">{{btnShow}}</button>
				<text>{{getData('12')}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	import uniSwipeAction from '@/components/uni-swipe-action/uni-swipe-action.vue'
	import uniSwipeActionItem from '@/components/uni-swipe-action-item/uni-swipe-action-item.vue'
	import meSelect from '@/components/me-select/me-select.vue'
	export default {
		components: {
			uniSwipeAction,
			uniSwipeActionItem,
			meSelect
		},
		computed: {
			btnShow() {
				return this.isAllChoose ? '取消全选' : '全选'
			}
		},
		data: () => ({
			
			dataList:[
				{
					id:'1',
					strList:['xxx.jpg','yyy.png']
				},
				{
					id:'2',
					strList:['zzz.jpg','aaa.png']
				}
			],
			
			
			
			title: 'checkbox 复选框',
			isAllChoose: false,

			items: [{
					value: 'USA',
					name: '美国'
				},
				{
					value: 'CHN',
					name: '中国',
					checked: 'true'
				},
				{
					value: 'BRA',
					name: '巴西'
				},
				{
					value: 'JPN',
					name: '日本'
				},
				{
					value: 'ENG',
					name: '英国'
				},
				{
					value: 'FRA',
					name: '法国'
				}
			],
			// options: [ {
			// 	text: '删除	',
			// 	style: {
			// 		backgroundColor: '#FF4645'
			// 	}
			// }]

			options: {
				flags: ['id'], //设置需要返回的参数这个参数必须在 dataList 中的item中存在（不配置默认全部返回）
				itemCanSelect: true //是否开启点击列表页选择配置
			},
			dataList: [{
					id: "1",
					select: false
				},
				{
					id: "2",
					select: false
				},
				{
					id: "3",
					select: false
				},
			]
		}),
		methods: {
			handleAllChoose(e) {
				// 首先取反
				this.isAllChoose = !this.isAllChoose

				if (this.isAllChoose) {
					this.items.forEach((item) => {
						this.$set(item, 'checked', true)
					})
				}else{
					this.items.forEach((item) => {
						this.$set(item, 'checked', false)
					})
				}

			},
			checkboxChange: function(e) {
				let items = this.items
				let	values = e.detail.value;
				for (let i = 0, lenI = items.length; i < lenI; ++i) {
					const item = items[i]
					if (values.includes(item.value)) {
						this.$set(item, 'checked', true)
					} else {
						this.$set(item, 'checked', false)
					}
				}
			},
			changeModel() {
				this.$refs.meSelect.changeModel()
			},
			getSelectAll() {
				var result = this.$refs.meSelect.getSelectAll()
				console.log('当前全选：', result)
			},
			itemClick(e) {
				console.log('列表点击了：', e)
			},
			finish(e) {
				console.log('所有的选择：', e)
			},
			change(e) {
				console.log('发生改变了：', e)
			},
			onClick(e) {
				console.log('当前点击的是第' + e.index + '个按钮，点击内容是' + e.content.text)
				uni.showModal({
					title: '提示',
					content: '此操作不可逆，是否确认删除',
					success: (res) => {
						if (res.confirm) {
							console.log('用户点击确定');
						} else if (res.cancel) {
							console.log('用户点击取消');
						}
					}
				});
			},

		}
	}
</script>

<style lang="scss" scoped>
	.cont {
		// background-color: pink;
	}

	.item {
		border: 1px solid red;
	}

	.uni-list-cell {
		justify-content: flex-start
	}
</style>

<template>
	<view class="qiun-columns">
		<view class="qiun-charts"><canvas canvas-id="canvasID" id="canvasID" class="charts" @touchstart="handleTouchStart"></canvas></view>
	</view>
</template>

<script>
import uCharts from '@/components/u-charts/u-charts.js';

var canvaChart = null;
var _self;
export default {
	data: () => ({
		cWidth: '',
		cHeight: '',
		pixelRatio: 1,
		serverData: ''
	}),
	onLoad() {
		_self = this;
		this.cWidth = uni.upx2px(750);
		this.cHeight = uni.upx2px(500);
		// 获取图标数据
		this.geData();
	},
	methods: {
		getData() {
			_self.showChart('canvasRing', Ring);
		},
		showChart(canvasId, chartData) {
			canvaChart = new uCharts({
				$this: _self,
				canvasId: canvasId,
				type: 'map',
				fontSize: 11,
				padding: [0, 0, 0, 0],
				legend: {
					show: false
				},
				background: '#FFFFFF',
				pixelRatio: _self.pixelRatio,
				series: chartData.series,
				width: _self.cWidth * _self.pixelRatio,
				height: _self.cHeight * _self.pixelRatio,
				extra: {
					map: {
						border: true,
						borderWidth: 1,
						borderColor: '#666666',
						fillOpacity: 0.6
					}
				}
			});
		},
		handleTouchStart(e) {
			canvaChart.showToolTip(e, {
				format: function(item) {
					return item.name + ':' + item.data;
				}
			});
		}
	}
};
</script>

<style lang="scss" scoped>
page {
	background: #f2f2f2;
	width: 750upx;
	overflow-x: hidden;

	.qiun-columns {
		display: flex;
		flex-direction: column !important;

		.qiun-charts {
			width: 750upx;
			height: 500upx;
			background-color: #ffffff;

			.charts {
				width: 750upx;
				height: 500upx;
				background-color: #ffffff;
			}
		}
	}
}
</style>

<template>
	<!-- 平台来源 -->
	<div class="echarts" id="PlatformSourceChart"></div>
</template>

<script setup lang="ts">
// Echarts 为init（dom元素后的类型）
// EChartsOption 为 option 的类型
import { ECharts, EChartsOption, init } from "echarts";
// interface ChartProp {
// 	name: string;
// 	value: number;
// 	percentage: string;
// }
const initChart = (): ECharts => {
	const charEle = document.getElementById("PlatformSourceChart") as HTMLElement;
	const charEch: ECharts = init(charEle);
	const option: EChartsOption = {
		grid: {
			top: "25%",
			bottom: "10%"
		},
		tooltip: {
			trigger: "axis",
			axisPointer: {
				type: "shadow",
				label: {
					show: true
				}
			}
		},
		legend: {
			data: ["治愈数量"],
			top: "15%",
			textStyle: {
				color: "#ffffff"
			}
		},
		xAxis: {
			data: ["1月", "2月", "3月", "4月", "5月", "6月", "7月", "8月", "9月", "10月", "11月", "12月"],
			axisLine: {
				show: false //隐藏X轴轴线
			},
			axisTick: {
				show: false //隐藏X轴刻度
			},
			axisLabel: {
				show: true,
				color: "#ebf8ac" //X轴文字颜色
			}
		},
		yAxis: [
			{
				type: "value",
				name: "出院数量",
				nameTextStyle: {
					color: "#ebf8ac"
				},
				splitLine: {
					show: false
				},
				axisTick: {
					show: false
				},
				axisLine: {
					show: false
				},
				axisLabel: {
					show: true,
					color: "#ebf8ac"
				}
			},
			{
				type: "value",
				nameTextStyle: {
					color: "#ebf8ac"
				},
				position: "right",
				splitLine: {
					show: false
				},
				axisTick: {
					show: false
				},
				axisLine: {
					show: false
				},
				axisLabel: {
					show: true,
					formatter: "{value} %", //右侧Y轴文字显示
					color: "#ebf8ac"
				}
			},
			{
				type: "value",
				gridIndex: 0,
				min: 50,
				max: 100,
				splitNumber: 8,
				splitLine: {
					show: false
				},
				axisLine: {
					show: false
				},
				axisTick: {
					show: false
				},
				axisLabel: {
					show: false
				},
				splitArea: {
					show: true,
					areaStyle: {
						color: ["rgba(250,250,250,0.0)", "rgba(250,250,250,0.05)"]
					}
				}
			}
		],
		series: [
			{
				name: "治愈数量",
				type: "line",
				yAxisIndex: 1, //使用的 y 轴的 index，在单个图表实例中存在多个 y轴的时候有用
				smooth: true, //平滑曲线显示
				showAllSymbol: true, //显示所有图形。
				symbol: "circle", //标记的图形为实心圆
				symbolSize: 10, //标记的大小
				itemStyle: {
					//折线拐点标志的样式
					color: "#058cff"
				},
				lineStyle: {
					color: "#058cff"
				},
				areaStyle: {
					color: "rgba(5,140,255, 0.2)"
				},
				data: [102, 234, 322, 412, 416, 567, 324, 555, 556, 700, 811, 1200]
			}
		]
	};
	charEch.setOption(option, true);
	return charEch;
};
defineExpose({
	initChart
});
</script>
<style lang="scss" scoped>
.echarts {
	width: 100%;
	height: 100%;
}
</style>

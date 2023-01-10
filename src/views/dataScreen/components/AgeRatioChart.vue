<template>
	<!-- 重症病例top -->
	<div class="echarts" id="AgeRatioChart"></div>
</template>

<script setup lang="ts">
// Echarts 为init（dom元素后的类型）
// EChartsOption 为 option 的类型
import { ECharts, EChartsOption, init } from "echarts";
const initChart = (): ECharts => {
	const charEle = document.getElementById("AgeRatioChart") as HTMLElement;
	const charEch: ECharts = init(charEle);
	/* echarts colors */
	const option: EChartsOption = {
		title: {
			text: "2023年重症病例统计表",
			textStyle: {
				align: "center",
				color: "#fff",
				fontSize: 25
			},
			top: "3%",
			left: "10%"
		},
		// backgroundColor: "#0f375f",
		grid: {
			top: "25%",
			bottom: "10%" //也可设置left和right设置距离来控制图表的大小
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
			// data: ["销售水量", "主营业务"],
			top: "15%",
			textStyle: {
				color: "#ffffff"
			}
		},
		xAxis: {
			data: ["2022.7", "2022.8", "2022.9", "2022.10", "2022.11", "2022.12", "2023.1", "2023.2"],
			axisLine: {
				show: true, //隐藏X轴轴线
				lineStyle: {
					color: "#01FCE3"
				}
			},
			axisTick: {
				show: true //隐藏X轴刻度
			},
			axisLabel: {
				show: true,
				color: "#ebf8ac" //X轴文字颜色
			}
		},
		yAxis: [
			{
				type: "value",
				name: "数量",
				nameTextStyle: {
					color: "#ebf8ac"
				},
				splitLine: {
					show: false
				},
				axisTick: {
					show: true
				},
				axisLine: {
					show: true,
					lineStyle: {
						color: "#FFFFFF"
					}
				},
				axisLabel: {
					show: true,
					color: "#ebf8ac"
				}
			},
			{
				type: "value",
				//   name: "同比",
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
				//   name: "主营业务",
				color: "#66FFCC",
				type: "bar",
				barWidth: 15,
				data: [100, 245, 456, 300, 600, 800, 1100, 1200]
			}
		]
	};
	charEch.setOption(option);
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

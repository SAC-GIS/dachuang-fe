<template>
	<!-- 实时访问 -->
	<!-- <div class="actual-total">
		<div class="expect-total">可预约总量<i>999999</i>人</div>
		<div class="actual-total">
			<div class="actual-item" v-for="(item, index) in actualTotal.split('')" :key="index">
				{{ item }}
			</div>
			<div class="actual-item">人</div>
		</div>
	</div> -->
	<div class="echarts" id="RealTimeAccessChart"></div>
</template>

<script setup lang="ts">
// Echarts 为init（dom元素后的类型）
// EChartsOption 为 option 的类型
// import { ref, Ref } from "vue";
import { ECharts, init } from "echarts";
import { watch } from "vue";
import "echarts-liquidfill";
// const actualTotal: Ref<string> = ref("216908");
const props = defineProps({
	province: {
		type: String,
		default: () => "北京市"
	}
});
const arr: any = [
	{ name: "北京市", value: [12, 10, 11, 9, 10] },
	{ name: "四川省", value: [11, 12, 10, 8, 11] },
	{ name: "河北省", value: [8, 5, 7, 8, 12] },
	{ name: "广东省", value: [12, 10, 10, 8, 9] }
];
let datas: any = [];
watch(
	[props],
	(newVal, oldVal) => {
		console.log(props.province);
		for (let i = 0; i < arr.length; i++) {
			if (props.province == arr[i].name) {
				datas = arr[i].value;
			}
		}
		console.log("新值", newVal);
		console.log("旧值", oldVal);
		initChart();
	},
	{ deep: true, immediate: true }
);
// watch(
// 	() => props.province,
// 	(newVal, oldVal) => {
// 		console.log("新值", newVal);
// 		console.log("旧值", oldVal);
// 	},
// 	{ deep: true }
// );
const initChart = (): ECharts => {
	// let d1: any = {
	// 	"黑龙江": [],
	// 	"吉林": [],
	// 	"辽宁": [],
	// 	"内蒙古": [],
	// 	"北京": [],
	// 	"河北": [],
	// 	"山西": [],
	// 	"山东": [],
	// 	"陕西": [],
	// 	"河南": [],
	// 	"安徽": [],
	// 	"江苏": [],
	// 	"湖北": [],
	// 	"浙江": [],
	// 	"上海": [],
	// 	"天津": [],
	// 	"宁夏": [],
	// 	"甘肃": [],
	// 	"青海": [],
	// 	"新疆": [],
	// 	"西藏": [],
	// 	"云南": [],
	// 	"四川": [],
	// 	"重庆": [],
	// 	"贵州": [],
	// 	"广西": [],
	// 	"广东": [],
	// 	"湖南": [],
	// 	"江西": [],
	// 	"福建": [],
	// 	"台湾": [],
	// 	"海南": [],
	// 	"香港": []
	// };
	const charEle = document.getElementById("RealTimeAccessChart") as HTMLElement;
	const charEch: ECharts = init(charEle);
	const option = {
		title: {
			text: props.province
		},
		tooltip: {
			trigger: "axis"
		},
		grid: {
			top: "25%",
			bottom: "10%" //也可设置left和right设置距离来控制图表的大小
		},
		xAxis: {
			type: "category",
			boundaryGap: false,
			data: ["20230201", "20230202", "20230203", "20230204", "20230205"]
		},
		yAxis: {
			type: "value",
			name: "确诊人数"
		},
		series: [
			{
				name: "predict",
				type: "line",
				data: datas,
				markPoint: {
					data: [{ name: "最低", value: 10 }]
				},
				markLine: {
					data: [
						{ type: "average", name: "Avg" },
						[
							{
								symbol: "none",
								x: "90%",
								yAxis: "max"
							},
							{
								symbol: "circle",
								label: {
									position: "start",
									formatter: "Max"
								},
								type: "max",
								name: "最高点"
							}
						]
					]
				}
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
	height: calc(100% - 50px);
}
.actual-total {
	position: relative;
	display: flex;
	align-items: center;
	justify-content: flex-end;
	height: 50px;
	margin-top: 10px;
	margin-right: 4px;
	.actual-item {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 52px;
		height: 50px;
		margin-right: 1px;
		font-family: MetroDF;
		font-size: 32px;
		color: #66ffff;
		background: url("../images/total.png") no-repeat;
		background-size: 100% 100%;
		&:last-child {
			margin-right: 0;
			font-size: 22px;
		}
	}
	.expect-total {
		position: absolute;
		top: -30px;
		right: 5px;
		font-size: 14px;
		color: #ffffff;
		i {
			font-style: normal;
			font-style: oblique;
			color: #ff8100;
		}
	}
}
</style>

function handleWatch() { throw new Error("Function not implemented."); }

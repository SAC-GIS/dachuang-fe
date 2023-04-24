<template>
	<!-- 中国地图 -->
	<div class="map-ball"></div>
	<div class="echarts" id="mapChart"></div>
</template>

<script setup lang="ts">
// Echarts 为init（dom元素后的类型）
// EChartsOption 为 option 的类型
import { ECharts, init } from "echarts";
import echarts from "@/utils/echarts";
import mapJson from "../assets/china.json";
/* echarts sysmbol */
// let planePath: string =
// 	"path://M1705.06,1318.313v-89.254l-319.9-221.799l0.073-208.063c0.521-84.662-26.629-121.796-63.961-121.491c-37.332-0.305-64.482,36.829-63.961,121.491l0.073,208.063l-319.9,221.799v89.254l330.343-157.288l12.238,241.308l-134.449,92.931l0.531,42.034l175.125-42.917l175.125,42.917l0.531-42.034l-134.449-92.931l12.238-241.308L1705.06,1318.313z";
const initChart = (): ECharts => {
	const charEle = document.getElementById("mapChart") as HTMLElement;
	const charEch: ECharts = init(charEle);
	echarts.registerMap("china", mapJson as any);

	//把所有城市的位置和各月份疫情信息添加到数组里面
	let geoCoordMap: any = {
		黑龙江: [126.5363383, 45.80734693],
		吉林: [125.2866434, 43.85392591],
		辽宁: [123.4409403, 41.88958731],
		内蒙古: [111.7749771, 40.86165455],
		北京: [116.3892349, 39.94138347],
		河北: [115.422438, 38.97441078],
		山西: [112.5220474, 37.89008234],
		山东: [117.1143325, 36.66627107],
		陕西: [108.9405044, 34.43188934],
		河南: [113.6426529, 34.77551637],
		安徽: [117.2461685, 31.85662269],
		江苏: [120.8716568, 32.04306309],
		湖北: [114.3238052, 30.59778902],
		浙江: [119.6302017, 29.13063113],
		上海: [121.4539322, 31.29503989],
		天津: [117.3560318, 39.37470211],
		宁夏: [106.2049087, 38.51169302],
		甘肃: [103.8153824, 36.13127563],
		青海: [97.34443509, 37.44220945],
		新疆: [87.58857571, 43.87616769],
		西藏: [91.17011868, 29.69049859],
		云南: [102.8156265, 24.88400738],
		四川: [104.0460952, 30.58360306],
		重庆: [106.9112524, 29.44393675],
		贵州: [106.6311011, 26.66173062],
		广西: [108.3559545, 22.83141275],
		广东: [113.26135, 23.12978772],
		湖南: [112.9427465, 28.25071721],
		江西: [115.8651098, 28.69495848],
		福建: [119.3038305, 26.09086315],
		台湾: [121.5670141, 25.0503063],
		海南: [110.2181371, 20.0606117],
		香港: [114.0523657, 22.53745592]
	};
	//2020数据
	let d1: any = {
		黑龙江: 964,
		吉林: 157,
		辽宁: 351,
		内蒙古: 364,
		北京: 987,
		河北: 373,
		山西: 224,
		山东: 862,
		陕西: 507,
		河南: 1299,
		安徽: 993,
		江苏: 684,
		湖北: 68149,
		浙江: 1306,
		上海: 1516,
		天津: 309,
		宁夏: 75,
		甘肃: 182,
		青海: 18,
		新疆: 980,
		西藏: 1,
		云南: 230,
		四川: 853,
		重庆: 590,
		贵州: 147,
		广西: 264,
		广东: 2046,
		湖南: 1021,
		江西: 935,
		福建: 513,
		台湾: 799,
		海南: 171,
		香港: 8846
	};

	//2021数据
	let d2: any = {
		黑龙江: 2035,
		吉林: 589,
		辽宁: 795,
		内蒙古: 1186,
		北京: 1211,
		河北: 1458,
		山西: 266,
		山东: 1043,
		陕西: 2219,
		河南: 1641,
		安徽: 1009,
		江苏: 1625,
		湖北: 68317,
		浙江: 2016,
		上海: 3103,
		天津: 589,
		宁夏: 122,
		甘肃: 356,
		青海: 30,
		新疆: 981,
		西藏: 1,
		云南: 1817,
		四川: 1321,
		重庆: 611,
		贵州: 160,
		广西: 622,
		广东: 3457,
		湖南: 1222,
		江西: 959,
		福建: 1363,
		台湾: 17050,
		海南: 190,
		香港: 12666
	};
	//2022数据
	let d3: any = {
		黑龙江: 3035,
		吉林: 1589,
		辽宁: 1795,
		内蒙古: 2186,
		北京: 6211,
		河北: 7458,
		山西: 1266,
		山东: 1543,
		陕西: 2819,
		河南: 2641,
		安徽: 1509,
		江苏: 1925,
		湖北: 75317,
		浙江: 3016,
		上海: 8103,
		天津: 1589,
		宁夏: 622,
		甘肃: 1356,
		青海: 70,
		新疆: 1981,
		西藏: 100,
		云南: 2817,
		四川: 2321,
		重庆: 1611,
		贵州: 560,
		广西: 1220,
		广东: 6457,
		湖南: 4222,
		江西: 1959,
		福建: 2363,
		台湾: 27050,
		海南: 690,
		香港: 22666
	};
	//2023数据
	let d4: any = {
		黑龙江: 3535,
		吉林: 1789,
		辽宁: 1895,
		内蒙古: 2486,
		北京: 6711,
		河北: 7858,
		山西: 1566,
		山东: 1843,
		陕西: 2919,
		河南: 2841,
		安徽: 1709,
		江苏: 2025,
		湖北: 75617,
		浙江: 3416,
		上海: 8403,
		天津: 1689,
		宁夏: 652,
		甘肃: 1456,
		青海: 80,
		新疆: 2081,
		西藏: 150,
		云南: 2917,
		四川: 2521,
		重庆: 1811,
		贵州: 590,
		广西: 1520,
		广东: 6757,
		湖南: 4822,
		江西: 2059,
		福建: 2763,
		台湾: 27850,
		海南: 699,
		香港: 22866
	};
	let colors: any = [
		["#1DE9B6", "#F46E36", "#04B9FF", "#5DBD32", "#FFC809", "#FB95D5", "#BDA29A", "#6E7074", "#546570", "#C4CCD3"],
		[
			"#37A2DA",
			"#67E0E3",
			"#32C5E9",
			"#9FE6B8",
			"#FFDB5C",
			"#FF9F7F",
			"#FB7293",
			"#E062AE",
			"#E690D1",
			"#E7BCF3",
			"#9D96F5",
			"#8378EA",
			"#8378EA"
		],
		["#DD6B66", "#759AA0", "#E69D87", "#8DC1A9", "#EA7E53", "#EEDD78", "#73A373", "#73B9BC", "#7289AB", "#91CA8C", "#F49F42"]
	];
	let colorIndex: any = 0;
	let year: any = ["2020", "2021", "2022", "2023"];
	let mapData: any = [[], [], [], [], [], [], []];

	/*柱子Y名称*/
	let categoryData: any = [];
	let barData: any = [];

	for (let key in geoCoordMap) {
		mapData[0].push({
			month: "2",
			name: key,
			value: d1[key]
		});
		mapData[1].push({
			month: "3",
			name: key,
			value: d2[key]
		});
		mapData[2].push({
			month: "4",
			name: key,
			value: d3[key]
		});
		mapData[3].push({
			month: "5",
			name: key,
			value: d4[key]
		});
	}

	for (let i = 0; i < mapData.length; i++) {
		// mapData[i].sort(function sortNumber(a: any, b: any) {
		// 	return a.value - b.value;
		// });
		barData.push([]);
		categoryData.push([]);
		for (let j = 0; j < mapData[i].length; j++) {
			barData[i].push(mapData[i][j].value);
			categoryData[i].push(mapData[i][j].name);
		}
	}

	let convertData: any = function (data: any) {
		let res = [];
		for (let i = 0; i < data.length; i++) {
			let geoCoord = geoCoordMap[data[i].name];
			if (geoCoord) {
				res.push({
					name: data[i].name,
					value: geoCoord.concat(data[i].value)
				});
			}
		}
		console.log(res);
		return res;
	};

	const optionXyMap01: any = {
		timeline: {
			data: year,
			axisType: "category",
			autoPlay: true,
			playInterval: 3000,
			left: "10%",
			right: "10%",
			bottom: "3%",
			width: "80%",
			label: {
				normal: {
					textStyle: {
						color: "#ddd"
					}
				},
				emphasis: {
					textStyle: {
						color: "#fff"
					}
				}
			},
			symbolSize: 10,
			lineStyle: {
				color: "#555"
			},
			checkpointStyle: {
				borderColor: "#777",
				borderWidth: 2
			},
			controlStyle: {
				showNextBtn: true,
				showPrevBtn: true,
				normal: {
					color: "#666",
					borderColor: "#666"
				},
				emphasis: {
					color: "#aaa",
					borderColor: "#aaa"
				}
			}
		},
		baseOption: {
			animation: true,
			animationDuration: 1000,
			animationEasing: "cubicInOut",
			animationDurationUpdate: 1000,
			animationEasingUpdate: "cubicInOut",
			grid: {
				right: "10%",
				top: "15%",
				bottom: "10%",
				width: "20%"
			},
			// tooltip: {
			// 	trigger: "axis", // hover触发器
			// 	axisPointer: {
			// 		// 坐标轴指示器，坐标轴触发有效
			// 		type: "shadow", // 默认为直线，可选为：'line' | 'shadow'
			// 		shadowStyle: {
			// 			color: "rgba(150,150,150,0.1)" //hover颜色
			// 		}
			// 	}
			// },
			tooltip: {
				trigger: "item",
				formatter: function (params: any) {
					if (params.data != undefined) {
						//由于下方的data数据拿错了导致这里显示undefine，在此重新修改了一下
						return params.data.name + " : " + params.data.value[2];
					}
				}
			},
			// visualMap: {
			// 	min: 0,
			// 	max: 100,
			// 	splitNumber: 5,
			// 	inRange: {
			// 		color: ["#d94e5d", "#eac736", "#50a3ba"].reverse()
			// 	},
			// 	textStyle: {
			// 		color: "#fff"
			// 	}
			// },
			geo: {
				show: true,
				map: "china",
				roam: true,
				zoom: 1,
				center: [105.83531246, 34.0267395887],
				label: {
					emphasis: {
						show: false
					}
				},
				itemStyle: {
					//地图颜色
					normal: {
						borderColor: "rgba(147, 235, 248, 1)",
						borderWidth: 1,
						areaColor: {
							type: "radial",
							x: 0.5,
							y: 0.5,
							r: 0.8,
							colorStops: [
								{
									offset: 0,
									color: "rgba(143, 235, 231, 0)" // 0% 处的颜色
								},
								{
									offset: 1,
									color: "rgba(143, 235, 231, .2)" // 100% 处的颜色
								}
							],
							globalCoord: false // 缺省为 false
						},
						shadowColor: "rgba(128, 217, 248, 1)",
						// shadowColor: 'rgba(255, 255, 255, 1)',
						shadowOffsetX: -2,
						shadowOffsetY: 2,
						shadowBlur: 10
					},
					emphasis: {
						areaColor: "#389BB7",
						borderWidth: 0
					}
				}
			}
		},
		options: []
	};

	for (let n = 0; n < year.length; n++) {
		optionXyMap01.options.push({
			// backgroundColor: "#013954",
			title: [
				{
					text: "2020年起全国新冠疫情发展情况",
					left: "23%",
					top: "7%",
					textStyle: {
						color: "#fff",
						fontSize: 25
					}
				}
			],

			series: [
				//地图
				{
					type: "map",
					map: "china",
					geoIndex: 0,
					aspectScale: 0.75, //长宽比
					showLegendSymbol: false, // 存在legend时显示
					label: {
						normal: {
							show: false
						},
						emphasis: {
							show: false,
							textStyle: {
								color: "#fff"
							}
						}
					},
					roam: true,
					itemStyle: {
						normal: {
							areaColor: "#031525",
							borderColor: "#FFFFFF"
						},
						emphasis: {
							areaColor: "#2B91B7"
						}
					},
					animation: false,
					data: mapData
				},
				// 地图中闪烁的点
				{
					//  name: 'Top 5',
					type: "effectScatter",
					coordinateSystem: "geo",
					// symbol: "pin", //气泡
					data: convertData(mapData[n]),
					symbolSize: function (val: any) {
						return val[2] / 500;
					},
					showEffectOn: "render",
					rippleEffect: {
						brushType: "stroke"
					},
					hoverAnimation: true,
					label: {
						normal: {
							formatter: "{b}",
							position: "right",
							show: true
						}
					},
					itemStyle: {
						normal: {
							color: colors[colorIndex][n],
							shadowBlur: 10,
							shadowColor: colors[colorIndex][n]
						}
					},
					zlevel: 1
				}
			]
		});
	}
	charEch.setOption(optionXyMap01);
	//点击前解绑，防止点击事件触发多次
	charEch.off("click");
	charEch.on("click", echartsMapClick);
	return charEch;
};
defineExpose({
	initChart
});
//echarts点击事件
const emits = defineEmits(["sendProvince"]);
function echartsMapClick(params: any) {
	// alert(params.data);
	emits("sendProvince", params.name);
}
</script>
<style lang="scss" scoped>
.echarts {
	width: 100%;
	height: 100%;
}
.map-ball {
	position: absolute;
	top: 50%;
	left: 50%;
	width: 900px;
	height: 900px;
	transform: translate(-50%, -50%);
	img {
		width: 500px;
		height: 500px;
	}
}
</style>

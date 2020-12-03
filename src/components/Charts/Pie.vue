<template>
    <div class="chart-container-pie">

    </div>
</template>

<script>
import echarts from 'echarts'

const chartPieColors = [
    [{
            offset: 0,
            color: "red" // 0% 处的颜色
        },
        {
            offset: 1,
            color: "#000" // 100% 处的颜色
        }
    ],
    [{
            offset: 0,
            color: "red" // 0% 处的颜色
        },
        {
            offset: 1,
            color: "#000" // 100% 处的颜色
        }
    ],
    [{
            offset: 0,
            color: "#AE60FA" // 0% 处的颜色
        },
        {
            offset: 1,
            color: "#6D32C1" // 100% 处的颜色
        }
    ],
    [{
            offset: 0,
            color: "#EFCE49" // 0% 处的颜色
        },
        {
            offset: 1,
            color: "#D79C12" // 100% 处的颜色
        }
    ],
    [{
            offset: 0,
            color: "#FFB058" // 0% 处的颜色
        },
        {
            offset: 1,
            color: "#C56625" // 100% 处的颜色
        }
    ],
    [{
            offset: 0,
            color: "#4ACC88" // 0% 处的颜色
        },
        {
            offset: 1,
            color: "#27A657" // 100% 处的颜色
        }
    ],
    [{
            offset: 0,
            color: "#2C989E" // 0% 处的颜色
        },
        {
            offset: 1,
            color: "#27BCC9" // 100% 处的颜色
        }
    ],
    [{
            offset: 0,
            color: "#8A98FF" // 0% 处的颜色
        },
        {
            offset: 1,
            color: "#2B36A8" // 100% 处的颜色
        }
    ]
]
const datas = [
    {value: 335, name: '直接访问'},
    {value: 310, name: '邮件营销'},
    {value: 274, name: '联盟广告'},
    {value: 235, name: '视频广告'},
    {value: 400, name: '搜索引擎'}
]

const seriesData = datas.map((item, index) => {
    return {
        value: item.value,
        name: item.name,
        itemStyle: {
            type: "linear",
            x: 0,
            y: 0,
            x2: 1,
            y2: 1,
            colorStops: chartPieColors[index > 8 ? Math.floor(Math.random() * 8 + 1) : index],
            global: false
        }
    }
})
console.log(seriesData)
const option = {
    tooltip: {
        trigger: 'item',
        formatter: '{a} <br/>{b} : {c} ({d}%)'
    },
    series: [
        {
            name: '访问来源',
            type: 'pie',
            radius: '55%',
            center: ['50%', '50%'],
            roseType: 'radius',
            label: {
                formatter: '{a} {c}'
            },
            data: seriesData,
            animationType: 'scale',
            animationEasing: 'elasticOut',
            animationDelay: function (idx) {
                return Math.random() * 200;
            }
        }
    ]
}

const data = [
    {id: 0, value: 335, name: '直接访问'},
    {id: 1, value: 310, name: '邮件营销'},
    {id: 2, value: 274, name: '联盟广告'},
    {id: 3, value: 235, name: '视频广告'},
    {id: 4, value: 400, name: '搜索引擎'}
]

export default {
    name: 'Pie',
    mounted () {
        const myChart = echarts.init(document.querySelector('.chart-container-pie'))
        setTimeout(() => {
            option.series[0].data = data
            console.log(option)
            myChart.setOption(option, true)
        }, 2000)
    }
}
</script>

<style>
    .chart-container-pie {
        width: 100%;
        height: 100%;
        min-height: 260px;
    }
</style>
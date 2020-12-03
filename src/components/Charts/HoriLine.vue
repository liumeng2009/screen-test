<template>
    <div class="chart-container-line">

    </div>
</template>

<script>
import echarts from 'echarts'

const option = {
    tooltip: {
        trigger: 'axis',
        axisPointer: {
            type: 'shadow'
        }
    },
    grid: {
        top: 0,
        left: '3%',
        right: '4%',
        bottom: '3%',
        containLabel: true
    },
    xAxis: {
        type: 'value',
        axisLabel: {
            color: '#5CE4FF'
        }
    },
    yAxis: {
        type: 'category',
        data: [ '24:00', '22:00', '20:00','18:00', '16:00','14:00', '12:00','10:00', '08:00','06:00', '04:00','02:00', '00:00'],
        axisLabel: {
            color: '#5CE4FF'
        }
    },
    series: [
        {
            type: 'bar',
            barWidth: 10,
            itemStyle: {
                color: {
                    type: 'linear',
                    x: 0,
                    y: 0,
                    x2: 1,
                    y2: 0,
                    colorStops: [{
                        offset: 0, color: '#43F85D' // 0% 处的颜色
                    }, {
                        offset: 1, color: '#E10019' // 100% 处的颜色
                    }],
                    global: false // 缺省为 false
                },
                barBorderRadius: [0, 10, 10, 0]
            }
        }
    ]
}

const data = [
    {time: '00:00', value: 50},
    {time: '02:00', value: 5},
    {time: '04:00', value: 10},
    {time: '06:00', value: 13},
    {time: '08:00', value: 18},
    {time: '10:00', value: 1},
    {time: '12:00', value: 69},
    {time: '14:00', value: 80},
    {time: '16:00', value: 12},
    {time: '18:00', value: 60},
    {time: '20:00', value: 44},
    {time: '22:00', value: 32},
    {time: '24:00', value: 100}
]

export default {
    name: 'HoriLine',
    mounted () {
        const myChart = echarts.init(document.querySelector('.chart-container-line'))
        setTimeout(() => {
            option.series[0].data = data
            myChart.setOption(option, true)
        }, 2000)
    }
}
</script>

<style>
    .chart-container-line {
        width: 100%;
        height: 100%;
        min-height: 425px;
    }
</style>
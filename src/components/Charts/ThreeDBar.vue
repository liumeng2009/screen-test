<template>
  <div class="chart-container-3d-bar">

  </div>
</template>

<script>
import echarts from 'echarts'
import 'echarts-gl'

const data = [
  { date: '5.1', app: 7, move: 7 },
  { date: '5.2', app: 3, move: 3 },
  { date: '5.3', app: 0, move: 2 },
  { date: '5.4', app: 1, move: 1 },
  { date: '5.5', app: 8, move: 9 },
  { date: '5.6', app: 4, move: 1 },
  { date: '5.7', app: 5, move: 2 },
]

var option = {
  xAxis3D: {
    type: 'category',
    name: '',
    splitLine: {
        show: false
    },
    splitArea: {
        show: false
    },
    axisPointer: {
        show: false
    },
    axisLine: {
        lineStyle: {
            opacity: 0
        }
    },
    axisTick: {
        lineStyle: {
            opacity: 0
        }
    },
    axisLabel: {
        margin: 10,
        textStyle: {
            color: '#5CE4FF'
        }
    }
  },
  legend: {},
  yAxis3D: {
    type: 'category',
    name: '',
    data: [''],
    splitLine: {
        show: false
    },
    axisTick: {
        lineStyle: {
            opacity: 0
        }
    }
  },
  zAxis3D: {
    type: 'value',
    name: '',
    axisLabel: {
        show: true,
        margin: 10,
        textStyle: {
            color: '#5CE4FF'
        }
    },
    axisLine: {
        lineStyle: {
            opacity: 0
        }
    },
    axisTick: {
        lineStyle: {
            opacity: 0
        }
    },
    splitLine: {
        show: true,
        lineStyle: {
            color: '#08416B',
            width: 1
        }
    }
  },
  grid3D: {
    show: true,
    boxWidth: 100,
    boxDepth: -20,
    boxHeight: 100,
    light: {
      main: {
        intensity: 1.2
      },
      ambient: {
        intensity: 0.3
      }
    },
    viewControl: {
      projection: 'orthographic',
      alpha: 10,
      beta: 10,
      maxOrthographicSize: 120,
      minOrthographicSize: 120
    },
    axisPointer: {
        show: false
    }
  },
  series: [
    {
      type: 'bar3D',
      barSize: 9,
      data: [
        [0, 0, 0.1],
        [1, 0, 0.1],
        [2, 0, 0.1],
        [3, 0, 0.1],
        [4, 0, 0.1],
        [5, 0, 0.1],
        [6, 0, 0.1]
      ],
      itemStyle: {
        color: '#fff',
        opacity: 0
      },
      stack: 'stack',
      shading: 'lambert',
      emphasis: {
        label: {
          show: false
        }
      }
    },
    {
      type: 'bar3D',
      barSize: 9,
      itemStyle: {
        color: '#1b6bff',
        opacity: 1
      },
      stack: 'stack',
      shading: 'lambert',
      emphasis: {
        label: {
          show: false
        }
      }
    },
    {
      type: 'bar3D',
      barSize: 9,
      itemStyle: {
        color: '#36adff',
        opacity: 1
      },
      stack: 'stack',
      shading: 'lambert',
      emphasis: {
        label: {
          show: false
        }
      }
    }
  ]
}

export default {
  name: 'ThreeDBar',
  data () {
    return {
      isLoading: false
    }
  },
  mounted() {
    var myChart = echarts.init(document.querySelector('.chart-container-3d-bar'))
    setTimeout(() => {
      const { axisXData, appData, moveData } = this.createData();
      option.xAxis3D.data = axisXData
      option.series[1].data = appData
      option.series[2].data = moveData
      myChart.setOption(option, true)
    }, 2000)
  },
  methods: {
    createData() {
      // x轴数据
      const axisXData = []
      // app数据
      const appData = []
      // 出行数据
      const moveData = []
      data.forEach((item, index) => {
        axisXData.push(item.date)
        appData.push([index, 0, item.app])
        moveData.push([item.date, 0, item.move])
      })
      console.log(axisXData)
      console.log(appData)
      console.log(moveData)

      return {
        axisXData,
        appData,
        moveData
      }
    }
  }
}
</script>

<style scoped lang="scss">
.chart-container-3d-bar{
    position:absolute;
    top: 0px;
    left: 0;
    z-index: 2;
    width: 408px;
    height: 425px;
}
</style>

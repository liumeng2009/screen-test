<template>
    <div id="map"></div>
</template>

<script>
import echarts from 'echarts'
import bmap from 'echarts/extension/bmap/bmap'// eslint-disable-line
import 'echarts-gl'
import { mapStyle } from './mapStyle'

const data = [[
    { coord: [120.12322240845, 30.256064370321] },
    { coord: [120.14280555506, 30.256064370321] },
    { coord: [120.14280555506, 30.226125905084] },
    { coord: [120.12322240845, 30.226125905084] },
    { coord: [120.12322240845, 30.256064370321] }
]]

import BindPng from '@/assets/bing.png'
import WarningBindPng from '@/assets/bing2.png'
export default {
    name: 'CityMap',
    mounted () {
        setTimeout(() => {
            this.draw()
        },2000)
    },
    methods: {
        draw () {
            var lines = data.map(function (track) {
                return {
                    coords: track.map(function (seg, idx) {
                        return seg.coord
                    })
                }
            })
            const myChart = echarts.init(document.getElementById('map'))
            myChart.setOption({
                bmap: {
                    center: [120.13066322374, 30.240018034923],
                    zoom: 14,
                    roam: true,
                    mapStyleV2: {
                        styleJson: mapStyle
                    }
                },
                series: [
                    {
                        type: 'lines',
                        coordinateSystem: 'bmap',
                        data: lines,
                        polyline: true,
                        lineStyle: {
                            color: 'green',
                            opacity: 1,
                            width: 2
                        }
                    }, {
                        type: 'scatter',
                        coordinateSystem: 'bmap',
                        data: [
                            [120.13066322374, 30.240018034923, 'in'],
                            [120.14566322374, 30.240018034923, 'out']
                        ],
                        symbol: (value) => {
                            console.log(value)
                            if (value[2] && value[2] === 'in') {
                                return `image://` + BindPng
                            } else if (value[2] && value[2] === 'out'){
                                return `image://` + WarningBindPng
                            }
                            
                        },
                        symbolSize: function() {
                            return 50
                        }
                    }
                ]
            })

            console.log(myChart)
        }
    }
}
</script>

<style lang="scss">
#map{
    width: 100%;
    height: 100%;
    background: #d1d1d1;
}

.anchorBL{
    display: none;
}
</style>

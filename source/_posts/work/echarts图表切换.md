---
title: Echarts切换图表-toolbox.feature使用官方的/自定义
date: 2022-04-25 21:32:01
tags:
  - Echarts
  - 场景错误
categories: work
---

# Echarts切换图表-toolbox.feature使用官方的/自定义

#### 1.柱状图和折线图可以通过官方的magicType来进行切换

```javascript
feature: {
  magicType: 
    {
      type: 
        ['line', 'bar'] //图表类型切换
     }
  ,
}, 

```

#### 2.但是饼状图不行，需要在里面自定义函数，如下

```javascript
<template>
  <div class="w-full h-full">
    <v-chart :options="options">
    </v-chart>
  </div>
</template>

<script>
import ECharts from 'vue-echarts'
import 'echarts/lib/component/legend'
import 'echarts/lib/component/title'
import 'echarts/lib/component/tooltip'
import 'echarts/lib/component/toolbox'
import 'echarts/lib/chart/line'
import 'echarts/lib/chart/pie'

export default {
  components: {
    'v-chart': ECharts
  },
  props: {
    chartsData: {
      type: Object
    }
  },
  data() {
    return {
      ProjectData: [],
      options: {},
    }
  },
  mounted() {
    this.getList()
  },
  methods: {
    getList() {
      // 按项目数据
      // this.ProjectData=this.chartsData.ProjectData
      this.ProjectData = [
        { value: 1048, name: 'Search Engine' },
        { value: 735, name: 'Direct' },
        { value: 580, name: 'Email' },
        { value: 484, name: 'Union Ads' },
        { value: 300, name: 'Video Ads' }]
      this.$nextTick(function () {
        this.BarChange()
        // this.randerEcharts()
      })
    },
    // 变为饼状图
    BarChange() {
      // 这里怎么传数据传5个图的呢
      let echartsData = this.ProjectData.map(item => {
        return {
          value: item.value,
          name: item.name
        }
      })
      let that = this
      that.options = {
        tooltip: {
          trigger: 'item',
          // 提示格式
          formatter: '{a} <br/>{b} : {c}个 ({d}%)',
        },
        toolbox: {
          show: true,
          feature: {
            dataView: { show: true, readOnly: false },
            myLineTool: {
              show: true,
              title: '切换为折线图',
              icon: 'path://M163.84 880.64h122.88v-737.28h-122.88v737.28z m-40.96-778.24h204.8v819.2h-204.8v-819.2z m286.72 204.8h204.8v614.4h-204.8v-614.4z m40.96 573.44h122.88v-532.48h-122.88v532.48z m245.76-368.64h204.8v409.6h-204.8v-409.6z m40.96 368.64h122.88v-327.68h-122.88v327.68z',
              onclick: function () {
                that.LineChange()
                // that.randerEcharts()
              }
            },
            myPieTool: {
              show: true,
              title: '切换为饼状图',
              icon: 'path://M512 0a512 512 0 1 0 512 512A512 512 0 0 0 512 0z m460.1856 489.8816H537.6V52.0192a461.2096 461.2096 0 0 1 434.5856 437.8624z m0 51.2a458.752 458.752 0 0 1-93.3888 249.4464L582.0416 541.0816zM512 972.8a460.8 460.8 0 0 1-25.6-921.6v464.2816a25.8048 25.8048 0 0 0 9.8304 20.48L845.6192 829.44a459.776 459.776 0 0 1-333.6192 143.36z',
              onclick: function () {
                that.BarChange()
                // that.randerEcharts()
              }
            },
          }
        },
        legend: {
          orient: 'vertical',
          left: 'left',
        },
        series: [
          {
            name: 'Access From',
            type: 'pie',
            // 半径&位置
            radius: "80%",
            center: ['50%', '50%'],
            data: echartsData,
            emphasis: {
              itemStyle: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: 'rgba(0, 0, 0, 0.5)'
              }
            }
          }
        ]
      }
    },
    // 变为线形图
    LineChange() {
      let lineData = this.ProjectData
      let xList = lineData.map(item => item.name)
      let data = lineData.map(item => item.value)
      let that = this
      that.options = {
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross'
          }
        },
        legend: {
          orient: 'vertical',
          left: 'left',
        },
        toolbox: {
          show: true,
          feature: {
            myTool1: {
              show: true,
              title: '切换为折线图',
              icon: 'path://M163.84 880.64h122.88v-737.28h-122.88v737.28z m-40.96-778.24h204.8v819.2h-204.8v-819.2z m286.72 204.8h204.8v614.4h-204.8v-614.4z m40.96 573.44h122.88v-532.48h-122.88v532.48z m245.76-368.64h204.8v409.6h-204.8v-409.6z m40.96 368.64h122.88v-327.68h-122.88v327.68z',
              onclick: function () {
                that.LineChange()
              }
            },
            myTool: {
              show: true,
              title: '切换为饼状图',
              icon: 'path://M512 0a512 512 0 1 0 512 512A512 512 0 0 0 512 0z m460.1856 489.8816H537.6V52.0192a461.2096 461.2096 0 0 1 434.5856 437.8624z m0 51.2a458.752 458.752 0 0 1-93.3888 249.4464L582.0416 541.0816zM512 972.8a460.8 460.8 0 0 1-25.6-921.6v464.2816a25.8048 25.8048 0 0 0 9.8304 20.48L845.6192 829.44a459.776 459.776 0 0 1-333.6192 143.36z',
              onclick: function () {
                that.BarChange()
              }
            },
          }
        },
        xAxis: {
          type: 'category',
          data: xList
        },
        yAxis: {
          type: 'value',
          axisLine: {
            show: true,
          },
        },
        series: [
          {
            data: data,
            type: 'bar',
            name: '数量',
            barMaxWidth: 22
          }
        ]
      }
    },
  },

}
</script>

<style>
.echarts {
  width: 100%;
  height: 100%;
}
</style>
```


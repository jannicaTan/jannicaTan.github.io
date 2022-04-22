---
title: element-ui/tab栏切换再加载问题
date: 2022-04-22 20:21:33
tags: 
  - VUE
  - 场景错误
categories:
---
### 错误1：切换tab栏发现echarts组件缩放失效

解决方式：

```bash
el-tab中的lazy属性，可以在切换的时候重新渲染
```

### 错误2：el-tab延迟加载
lazy属性解决了echarts的显示问题，但是我发现当你把全部tab栏全部切换一遍之后，再切换就不重新渲染了...我的子组件就拿不到数据了

解决方式：为tab-panel添加key属性，v-if判断当前激活的tab内容，这样就不会同时把其他的也渲染出来，需要哪个渲染哪个。

```vue
 <el-tabs v-model="activeName" @tab-click="handleClick">
          <el-tab-pane v-for="(item,index) in tabsArr" :key="index" :label="item.label" :name="item.name">
            <SettleTabData :settleData="settleData" v-if="item.name == activeName"></SettleTabData>
          </el-tab-pane>
 </el-tabs>
```

```javascript
  data() {
    return {
      tabsArr: [
        {
          label:"待审批", name:"first"
        },
        {
          label:"待支付", name:"second"
        },
        {
          label:"已支付", name:"third"
        },
        {
          label:"全部", name:"fourth"
        }
      ],
      activeName: 'second',
      settleData: ['second', 'month'],
      date: ['', ''],
      status: 'month'
    }
  },
 methods: {
    // tab切换
    handleClick() {
      console.log('activeName', this.activeName)
      this.settleData[0] = this.activeName
    }
  },
```
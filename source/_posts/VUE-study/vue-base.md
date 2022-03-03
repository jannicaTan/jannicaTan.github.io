---
title: vue基础——特性/指令/过滤器/侦听器/计算属性
date: 2022-02-27 21:56:37
tags: VUE
categories: VUE
---

## VUE特性

- ① 数据驱动视图：

  - 优点：当页面数据发生变化时，页面会自动重新渲染页面的结构

  - ⚠️注意：数据驱动视图是单向的数据绑定。

-  ② 双向数据绑定
  - 优点：不操作 DOM 的前提下，自动把用户填写的内容同步到数据源中

## MVVM——Model、View 、 ViewModel

- 具体结构

  - Model 表示当前页面渲染时所依赖的数据源。

  - View 表示当前页面所渲染的 DOM 结构。

  - ViewModel 表示 vue 的实例，它是 MVVM 的核心。

- 工作原理

  - 当数据源发生变化时，会被 ViewModel 监听到，VM 会根据最新的数据源自动更新页面的结构

  - 当表单元素的值发生变化时，也会被 VM 监听到，VM 会把变化过后最新的值自动同步到 Model 数据源中

- MVVM具体结构的对应关系![img](https://api2.mubu.com/v3/document_image/2e31dec3-f22c-4e2d-add4-231fb6a4a0f9-17016005.jpg)

## VUE指令

- ① 内容渲染指令

  - v-text：

    - 放在标签内使用,只渲染纯文本

    - v-text 指令会覆盖元素内默认的值。

  -  插值表达式——`{{msg}}`
  
    - 它不会覆盖元素中默认的文本内容，只渲染纯文本

    - ⚠️：除了支持绑定简单的数据值之外，还支持 Javascript 表达式的运算:三元表达式/数字计算/数组修改

  - v-html
    - 将包含 HTML 标签的字符串渲染为页面的 HTML 元素

- ② 属性绑定指令——v-bind/：
  - 为元素的属性动态单向绑定属性值

- ③ 事件绑定指令——v-on/@

  - 为 DOM 元素绑定事件监听,eg:：@click、 @input、@keyup

  - 绑定的事件处理函数，需要在 methods 节点中进行声明

  - 常用事件修饰符——@event.事件修饰符![img](https://api2.mubu.com/v3/document_image/54eb416a-19e7-4a77-b2df-60f27ddc3529-17016005.jpg)

  - 按键修饰符——.enter .tab .delete (捕获“删除”和“退格”键) .esc .space .up .down .left .right

  - 事件对象$event

    - 注意在事件中要使用 $event 符号

    - 获取当前事件元素：e.target

- ④ 双向数据绑定指令——v-model
  - 常用修饰符![img](https://api2.mubu.com/v3/document_image/2265d85c-0848-4d0e-9c75-b824c1c1615b-17016005.jpg)

- ⑤ 条件渲染指令——v-if/v-show

  - 实现原理

    - v-if 指令会动态地创建或移除 DOM 元素，从而控制元素在页面上的显示与隐藏, 有更高的切换开销；

    - v-show 指令会动态为元素添加或移除 style="display: none;" 样式，从而控制元素的显示与隐藏,更高的初始渲染开销；

  - 实际使用

    - 如果需要非常频繁地切换——使用 v-show

    - 如果在运行时条件很少改变——使用 v-if

- ⑥ 列表渲染指令——v-for

  - `<tr v-for="(item, index) in list" :key="item.id"></td>`

  - 索引

    - 这里仅仅指的是它当前的位置，而不是绑定的元素/数据

    - v-for 指令中的 item 项和 index 索引都是形参，可以根据需要进行重命名。例如 (user, i) in userlist

  - 维护列表的状态——key

    - key 的值只能是字符串或数字类型 key 的值必须具有唯一性（即：key 的值不能重复）

    - 建议把数据项 id 属性的值作为 key 的值（因为 id 属性的值具有唯一性） 

    - 使用 index 的值当作 key 的值没有任何意义（因为 index 的值不具有唯一性）

    -  建议使用 v-for 指令时一定要指定 key 的值（既提升性能、又防止列表状态紊乱）

## 文本格式化——过滤器:filters()

- 基本用法:

  - 本质上是函数，需定义在fliters下

  - 在过滤器函数中，一定要有 return 值

  - 在html语句中的插值表达式内利用管道符插入相关处理函数： `<p>message 的值是：{{ message | capi }}</p>`

  -  ⚠️注意：过滤器函数形参可以有其他的参数，但是其默认的第一参数—— val，永远都是“管道符”前面的那个值

- 过滤器分类

  - 全局过滤器

    - 具体格式：`Vue.filter('过滤器名称', function (参数){ } ) `

    - 优点：具有复用性

  - 私有过滤器：直接在vm中调用

- 调用原则——就近：如果全局过滤器和私有过滤器名字一致，此时按照“就近原则”，调用的是”私有过滤器“

- 未完成：完善案例：时间格式化

## 监视数据变化——侦听器:watch:{}

- 语法格式:侦听器本质上是一个函数，把数据名作为方法名。新值在前，旧值在后

- 侦听器格式：

  - 方法格式：

    - 具体格式参考：可以看到将数据dataname作为方法名(newVal)![img](https://api2.mubu.com/v3/document_image/aa8d9d7a-233f-4db6-bf9d-b93143371478-17016005.jpg)

    - 缺点：

      - 1：无法在刚进入页面的时候，自动触发

      - 2：如果侦听的数据data中是一个对象，如果对象中的属性发生了变化，不会触发侦听器！！！

  - 对象格式：

    - 具体格式参考：此时需要一个`handler(newVal,oldVal)`的处理函数进行传值![img](https://api2.mubu.com/v3/document_image/7565ec02-1474-47ce-be69-c7c70cdfcdf4-17016005.jpg)

    - 优点：

      - 1：侦听器自动触发—— immediate 选项
        - immediate为boolean类型，默认为false，如果为true则设置自动触发一次

      - 2：侦听器深度监听对象中每个属性的变化—— deep 选项

        - deep选项为boolean类型，默认为false，如果为true，只要对象中任何一个属性变化了，都会触发“对象的侦听器”

        - ⚠️注意：如果要单独侦听对象子属性的变化，则必须包裹一层单引号——'info.username'(newVal) {}

## 计算属性——computed()

- 定义的时候，要被定义为“方法”,但本质是一个属性

- 具体格式：写在`computed:{}`中，属性要定义为方法格式![img](https://api2.mubu.com/v3/document_image/418bd9a4-feb6-4ec8-9582-2f438b6998b8-17016005.jpg)

- 优点：

  - 实现了代码的复用

  - 只要计算属性中依赖的数据源变化了，则计算属性会自动重新求值！

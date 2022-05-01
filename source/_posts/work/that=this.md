---
title: vue中 let that=this的作用
date: 2022-04-27 09:14:46
tags: VUE
categories: work
---

最近在写图表切换的时候，发现设定echarts option往往先让that=this，然后再使用this，不知道为什么这样，所以记录一下：

**this 会随着上下文环境而变换它的指向**，在当前作用域中设置一个变量用来存储 this 可以<u>**防止在其他地方找不到 this 的错误**</u>

在Vue中this始终指向Vue，但一些其他组件如axios中this为undefined

通过 `let that = this   `将this保存在that中，再在函数中使用that均可


---
title: Webpack基础配置(待继续更新)
date: 2022-02-23 20:22:24
tags: Webpack
categories: 前端工程化
---

![前端工程化——Webpack](https://raw.githubusercontent.com/jannicaTan/image_picX/master/VUE-Study/前端工程化——Webpack.webp)

- ### 前端工程化

  - #### 模块化

    - js 的模块化、css 的模块化、资源的模块化

  - #### 组件化

    - 复用现有的 UI 结构、样式、行为

  - #### 规范化

    - 目录结构的划分、编码规范化、接口规范化、文档规范化、 Git 分支管理

  - #### 自动化

    - 自动化构建、自动部署、自动化测试

- ### Webpack

  - #### 概念

    - webpack 是前端项目工程化的具体解决方案。提供了友好的前端模块化开发支持，以及代码压缩混淆、处理浏览器端 JavaScript 的兼容性、性能优化等强大的功能。让程序员把工作的重心放到具体功能的实现上，提高了前端开发效率和项目的可维护性。

  - #### webpack全局安装

    - npm install webpack webpack-cli -D

  - #### webpack配置项

    - 在webpack.config.js中进行配置

    - webpack的基本配置项及插件配置![img](https://api2.mubu.com/v3/document_image/672bcb5a-142d-4521-83f4-b18e96122f07-17016005.jpg)

    - ##### 基本配置项

      - mode

        -  ① development — 开发环境 

          - 不会对打包生成的文件进行代码压缩和性能优化 

          - 打包速度快，适合在开发阶段使用

        -  ② production ——生产环境 

          -  会对打包生成的文件进行代码压缩和性能优化 

          - 打包速度很慢，仅适合在项目发布阶段使用

      - entry/output
        - 通过 entry 节点指定打包的入口。通过 output 节点指定打包的出口

    - ##### 插件配置项

      - 1 webpack-dev-server
        - 让 webpack 监听项目源代码的变化，从而进行自动打包构建。

      - 2 html-webpack-plugin
        - 通过 html-webpack-plugin 插件，将 src 目录下的 index.html 首页，复制到项目根目录中一份,将页面放入到内存中

      - 3 devServer
        - 控制打包后是否自动打开/访问路径/自定义端口号

    - ##### loader加载

      - 打包处理css

      - 打包处理less

      - 打包处理路径图片

      - 打包处理高级JS语法

  - #### SourceMap

    - 作用：
      精准定位到错误行并显示对应的源码 方便开发者调试源码中的错误

    - 开发实践

      - ① 开发环境下：

        - 把 devtool 的值设置为 eval-source-map

        - 好处：可以精准定位到具体的错误行

      - ② 生产环境下：

        - 建议关闭 Source Map 或将 devtool 的值设置为 nosources-source-map

        - 好处：防止源码泄露，提高网站的安全性

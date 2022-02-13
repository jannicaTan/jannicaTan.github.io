---
title: ES6-01-初始化
date: 2022-02-10 17:53:43
tags: ES6
categories: ES6
---

## 1.ES6初始化

1.1 模块化ES6(`node version>14.15.1`)

- 快速初始化包管理配置文件

```bash
npm init -p
```

- 生成package.json文件
- 在其中添加

```bash
"type": module
```

1.2 ES6模块化基本语法

- 默认导出与默认导入

  - 默认导出

    - ```js
      export default {导出对象}
      ```

    - 目的:挂载使外界能够访问导出的对象

    - ⚠️注意：只允许使用唯一的一次export default

  - 默认导入

    - ```js
      import 自定义变量名称 from ‘模块标识符/文件路径.js’
      ```

- 直接导入

  - 导入的时候直接import js文件路径 即可

- 按需导入与导出

  - 按需导出

    - ```js 
      export 导出的变量
      ```

  - 按需导入

    - import {按需导出的对应名称1,名称2....} from 对应js文件

  - ⚠️ 注意事项：

      1.可以多次按需导出

      2.按需导入的名称要与按需导出的名称保持一致

      3.可以使用as 重命名名称 进行重命名

      4.按需导入可以与默认导入一起

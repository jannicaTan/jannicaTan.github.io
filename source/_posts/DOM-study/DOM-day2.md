---
title: DOM_day2
date: 2022-01-17 11:21:02
tags: DOM学习-day2
categories: DOM学习
---

## 排他思想：

## 自定义属性操作：

### 获取元素的属性值

(1) `element.属性`——获取元素本身自带的内置属性

(2) `element.getAttribute('属性')`——获取自定义属性

​	 get得到获取 attribute 属性的意思，我们程序员自己添加的属性我们称为自定义属性 index

### 设置元素的属性值

 (1) `element.属性= '值'`——直接赋值

```js
div.id = 'test';
div.className = 'navs';
```

 (2) `element.setAttribute('属性', '值')`——针对于自定义属性

```js
div.setAttribute('index', 2);
```

### 移除属性——removeAttribute(属性)    

```js
div.removeAttribute('index');
```

### H5自定义属性命名——`data-开头`

#### dataset——存放了所有以data开头的自定义属性

dataset是一个集合，里面存放了所有以data开头的自定义属性，获取其中属性的操作如下：

⚠️：

- 如果自定义属性里面有多个-链接的单词，我们获取的时候采取 驼峰命名法
- IE11以上才可应用，兼容性不好

```js
console.log(div.dataset);
console.log(div.dataset.index);
console.log(div.dataset['index']);
```

## 节点操作:

一般地，节点至少拥有nodeType（节点类型）、nodeName（节点名称）和nodeValue（节点值）这三个基本属性

- 元素节点nodeType 为1
- 属性节点nodeType 为2
- 文本节点noueType 为多（文本节点包含文字、全修、接行等）


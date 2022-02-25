---
title: DOM-Day1-DOM元素
date: 2022-01-12 19:24:45
tags: DOM学习-day1
categories: DOM学习
---

### - DOM简介

#### - DOM树
![DOM树](https://cdn.jsdelivr.net/gh/jannicaTan/image_picX@master/DOM-study/DOM树.webp)

- 文档：document
- 标签：element
- 节点-内容：node 标签/属性/文本/注释等

------

### - 获取元素

#### - 根据ID获取——getElementById

- 参数
  - **`element`**是一个 [Element](https://developer.mozilla.org/zh-CN/docs/Web/API/Element) 对象。如果当前文档中拥有特定ID的元素不存在则返回null.
  - **`id`**是大小写敏感的字符串，代表了所要查找的元素的唯一ID.
- 返回值
  - 返回一个匹配到 ID 的 DOM [`Element`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element) 对象。若在当前 [`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document) 下没有找到，则返回 null。

#### - 根据tag获取——getElementsByTagName(标签名)

```javascript
    <script>
        // 1.返回的是 获取过来元素对象的集合 以伪数组的形式存储的
        var lis = document.getElementsByTagName('li');
        console.log(lis);
        console.log(lis[0]);
        // 2. 我们想要依次打印里面的元素对象我们可以采取遍历的方式,动态变化
        for (var i = 0; i < lis.length; i++) {
            console.log(lis[i]);

        }
        // 3. 如果页面中只有一个li 返回的还是伪数组的形式 
        // 4. 如果页面中没有这个元素 返回的是空的伪数组的形式

        // 5. element.getElementsByTagName('标签名'); 
				//    父元素必须是指定的单个元素,不能用伪数组形式作为父元素
				//    获取的时候不包括父元素本身
        // var ol = document.getElementsByTagName('ol'); // [ol]
        // console.log(ol[0].getElementsByTagName('li'));
        var ol = document.getElementById('ol');
        console.log(ol.getElementsByTagName('li'));
    </script>
```

#### - H5新增，不能兼容IE6/7/8的方法

##### - 通过类选择器获取元素——getElementByClassName()

```javascript
//根据类名获得某些元素集合
        var boxs = document.getElementsByClassName('box');
        console.log(boxs);
```

##### - 通过选择器获取元素

**querySelector()**返回指定选择器的**<u>第一个元素对象</u>**  

**querySelectorAll()**返回指定选择器的**<u>所有元素对象集合</u>**

⚠️里面的选择器需要加符号

- **class->'.box'** 
-  **id->'#nav'**

```js
        var firstBox = document.querySelector('.box');
        console.log(firstBox);
        var allBox = document.querySelectorAll('.box');
        console.log(allBox);
        var nav = document.querySelector('#nav');
        console.log(nav);
        var li = document.querySelector('li');
        console.log(li);
```

#### - 获取特殊元素

获取body——**document.body**

获取html——**document.documentElement**

------

### - 事件基础

#### - 事件三要素：事件源、事件类型和事件处理程序。

(1)事件源：事件被触发的对象，例如按钮
(2)事件类型：如何触发，例如鼠标点击(onclick)
(3)事件处理程序：通过一个函数赋值的方式完成

```javascript
    <button id='btn1'>1+1</button>
    <script>
        var btn1 =document.querySelector('#btn1');
        btn1.onclick=function(){
            alert('2');
        }
    </script>
```

![mousefunc](https://cdn.jsdelivr.net/gh/jannicaTan/image_picX@master/DOM-study/mousefunc.webp)

- 获得焦点事件——`onfocus` 
- 失去焦点事件——`onblur`

#### 执行事件三步骤：

```js
        // 1. 获取事件源
        var div = document.querySelector('div');
        // 2.绑定事件 注册事件
        // div.onclick 
        // 3.添加事件处理程序 
        div.onclick = function() {
            console.log('我被选中了');
        }
```

------

### - 操作元素

#### - 改变元素内容——innerText()/innerHTML()

##### - innerText 和 innerHTML的区别

| innerText                                    | innerHTML            |
| -------------------------------------------- | -------------------- |
| 不识别html标签 非标准                        | 识别html标签 W3C标准 |
| 这两个属性是可读写的  可以获取元素里面的内容                           |
| 去除空格和换行                               | 保留空格和换行       |

#### - 修改元素

##### - 表单input属性修改

常用属性：`type/value/checked/selected/disabled`

不可以用innerHTML了

#### - 样式属性操作——element.style/className

我们可以通过 JS 修改元素的大小、颜色、位置等样式。

- 行内样式：element.style，样式修改较少
- 类名样式：element.className，样式修改较多

⚠️注意：
1.JS 里面的样式采取驼峰命名法 比如 fontSize、 backgroundColor 

2.JS 修改 style 样式操作，产生的是行内样式，权重比较高

------

### 总结

![dom操作总结](https://cdn.jsdelivr.net/gh/jannicaTan/image_picX@master/DOM-study/dom操作总结.webp)

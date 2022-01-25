---
title: DOM-day4-高级事件
date: 2022-01-22 11:39:08
tags:
categories:
---



### 元素注册事件的两种方式

#### 1.传统注册事件——on开头

**<u>特点</u>**:注册时间具有唯一性 同一个元素的同一事件只能设置一个处理函数

#### 2.事件侦听注册事件——`addEventListener('事件类型',function(){},useCapture(true/false))`

**<u>特点:</u>**

 (1) 里面的事件类型是字符串 必定<u>加引号</u> 而且不带on

 (2) 同一个元素 同一个事件可以添加多个侦听器（事件处理程序）按顺序执行

### 删除事件的两种方式

#### 1.传统删除事件——`元素名.事件类型=null`

#### 2.常用——`元素名.removeEventListener('事件类型',注册事件方法名)`

#### 3.IE9以下老版本——`元素名.detachListener('事件类型',注册事件方法名)`

### DOM 事件流的三个阶段

#### 三个阶段 `捕获阶段->当前目标阶段->冒泡阶段`

1.**<u>捕获阶段</u>**: addEventListener 第三个参数是 true

顺着从大到小：`document -> html -> body -> father -> son `

点击相应,其他元素没有这个动作 则点击其他元素不会反应,依次向下寻找

2.**<u>冒泡阶段</u>**: addEventListener 第三个参数是 false/省略

顺着从小到大去找点击响应：`son -> father ->body -> html -> document`

### 事件对象——event事件

1. event 就是一个事件对象 写到我们侦听函数的 小括号里面 当形参来看

2. 事件对象只有有了事件才会存在，它是系统给我们自动创建的，不需要我们传递参数

3. 事件对象 是 我们事件的一系列相关数据的集合 跟事件相关的,

   ​	比如鼠标点击里面就包含了鼠标的相关信息：鼠标坐标

   ​	如果是键盘事件里面就包含的键盘事件的信息：判断用户按下了那个键

4. 这个事件对象我们可以自己命名 比如 event 、 evt、 e

5. 事件对象也有兼容性问题 ie678 

   通过 `window.event` 兼容性的写法  `e = e || window.event`;

```js
var div = document.querySelector('div');
div.addEventListener('click', function(e) {
  console.log(e);
})
```

### 常见事件对象的属性和方法

#### 1.`e.target`——返回的是触发事件的对象（元素）

与`this`的区别：

- `e.target` 点击了那个元素，就返回那个元素
- `this` 哪个元素绑定了这个点击事件，那么就返回绑定该事件的元素
- `e.srcElement`:适用于低版本:IE6/7/8

```js
var ul = document.querySelector('ul');
ul.addEventListener('click', function(e) {
  // 我们给ul 绑定了事件  那么this 就指向ul  
  console.log(this);//ul
  // e.target 指向我们点击的那个对象 谁触发了这个事件 我们点击的是li e.target 指向的就是li
  console.log(e.target);//li
  console.log(e.currentTarget);
            })
```

#### 2.`e.type`——返回当前触发的事件类型

#### 3.`e.preventDefault()`——阻止默认行为(事件)

实例：

- 点击超链接不跳转
- 点击提交按钮不提交

#### 4.重点：`e.stopPropagation()`——阻止冒泡

防止在底层事件触发上层事件

### 事件委托

**<u>原理</u>**：给父节点添加侦听器，而不给每个子节点单独设置监听器，利用事件冒泡传到父节点，影响每一个子节点

**<u>作用</u>**：只操作了一次DOM，提高了效率

**<u>实例</u>**：为父节点添加操作，用`e.target.具体元素内容`识别每次操作的子节点

```js
var ul=document.querySelector('ul');
ul.addEventListener('click',function(e){
  e.target.style.backgroundColor='pink'
})
```

### 鼠标事件对象——MouseEvent

进行相应的鼠标操作事件(click/onmouseover/onmouseout)后返回对应的坐标位置

#### 1.`e.clientX`/`e.clientY`——可视区坐标

#### 2.`e.pageX`/`e.pageY`——页面文档坐标(滚动页面)

滚动页面坐标也会变化的

#### 3.`e.screenX`/`e.screenY`——电脑屏幕坐标

**<u>案例</u>**：跟随鼠标的图标操作

### 键盘事件

进行相应的键盘操作所反馈的信息，执行顺序为:keydown->keypress->keyup

1.`keyup`——**<u>按下按键弹起后</u>**触发

2.`keypress`——按下按键即触发:**<u>无法识别功能键</u>**

3.`keydown`——按下按键即触发:**<u>识别功能键</u>**

### 键盘对象——`keyCode`

激发键盘事件后可以得到相应键的 ASCII码值

**<u>注意</u>**：

1. 我们的`keyup` 和`keydown`事件不区分字母大小写  a 和 A 得到的都是65

2. 我们的`keypress` 事件,区分字母大小写  a  97 和 A 得到的是65


---
title: 剑指Offer-09/30
date: 2022-05-11 20:46:10
tags: 
  -	LeetCode
  - 剑指offer
categories: Algorithm
---

## [剑指 Offer 09. 用两个栈实现队列](https://leetcode.cn/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

> 用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 `appendTail` 和 `deleteHead` ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，`deleteHead` 操作返回 -1 )

#### 示🌰：

```Bash
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```

#### 思路：

> 分别声明两个栈，A栈负责模拟入队，B栈负责模拟出队

```JavaScript
var CQueue = function() {
    this.stackA=[]
    this.stackB=[]
};
// 入队操作
CQueue.prototype.appendTail = function(value) {
    this.stackA.push(value)
};
// 出队操作
CQueue.prototype.deleteHead = function() {
    // 判断B是否为空
    if(this.stackB.length){
        return this.stackB.pop()
    }
    else{
        // B为空且A也为空，返回-1
        if(!this.stackA.length){
            return -1
        }
        // B为空但是A不为空，将A的值先依次出栈压入B中，然后B再pop
        else{
            while(this.stackA.length){
                this.stackB.push(this.stackA.pop())
            }
        } 
        return this.stackB.pop()
    }
    
};
```

## [剑指 Offer 30. 包含min函数的栈](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/)

> 定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

#### 示🌰：

```Bash
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

#### 思路：

> 声明两个栈，一个数据栈，一个单调递减的最小栈

1.入栈时，如果最小栈为空，或者新元素小于或等于最小栈栈顶，则将新元素压入最小栈，最小栈的**栈顶永远是最小元素** 2.出栈时，如果出栈元素和最小栈栈顶元素值相等，如果要弹出的元素同时存在于最小栈中，就一起弹出

```JavaScript
var MinStack = function() {
    this.stack=[]
    this.minstack=[]
};

MinStack.prototype.push = function(x) {
    this.stack.push(x)
    // 这里要判断等于x，只有最小栈为空，新元素 小于等于 最小栈栈尾，才移入，因为要维护单调栈
    if(!this.minstack.length||this.minstack[this.minstack.length-1]>=x){
        this.minstack.push(x)
    }
};

MinStack.prototype.pop = function() {
    // 方法1:用val来记录pop的值然后判断返回
    // let val=this.stack.pop()
    if(this.minstack[this.minstack.length-1]==this.stack.pop())   {
       return this.minstack.pop()
    }
    return this.stack.pop
};

MinStack.prototype.top = function() {
    // 返回stack的栈顶值
    return this.stack[this.stack.length-1]
};

MinStack.prototype.min = function() {
    // 返回minstack的栈顶值
    return this.minstack[this.minstack.length-1]
};
```

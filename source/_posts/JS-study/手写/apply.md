---
title: 手写call/apply/bind及理解
date: 2022-05-19 19:25:11
tags:  JS
categories: 
---

# 共同点：

##### 功能一致——可以函数体内的改变this指向

- 但是只是调用改变，本身不改变

- 语法： 函数.call()、函数.apply()、函数.bind()

# 区别

区别：

- call、apply可以立即执行。bind不会立即执行，因为bind返回的是一个函数需要加入()执行。![img](https://api2.mubu.com/v3/document_image/9400588d-a172-477a-8b3a-249fbef7ff1e-17016005.jpg)

- 参数不同：apply第二个参数是数组。call和bind有多个参数需要挨个写。![img](https://api2.mubu.com/v3/document_image/2f7875e8-40cf-45fd-9d38-8b268e10dcaf-17016005.jpg)

# 场景：一般用call

- Math.max数组求最大值：使用apply()![img](https://api2.mubu.com/v3/document_image/997d46a1-8298-49f4-b8f1-61767ca8e9a5-17016005.jpg)

- bind场景![img](../../../../../../Study-TensorFlow/Study-NLP/IMGassset/2fd03ffd-08ef-4e03-8d0c-54b58615445b-17016005.jpg)

# 手写一下

这里先写上一个用于改变指向的`function`

```js
function A(name, age) {
      this.name = name;
      this.age = age;
      this.hobby = function (...params) {
        console.log('name:', this.name, ',age:', this.age, 'params:', ...params)
      }
    }
const Aa = new A('haha', 18)
//一般调用
    Aa.hobby.call({
      name: 'feifei',
      age: 28
    })
```

## Call

```js
// 手写call
     Function.prototype.myCall = function (context, ...args) {
       context = context ? context : window
       context.fn = this
       var result = context.fn(...args)
       delete context.fn
       return result
     }

     Aa.hobby.myCall({
       name: 'feifei',
       age: 28
     }, 1, 3, 4)
```

## Apply

```js
// 手写apply
     Function.prototype.myApply = function (context, args) {
       context = context ? context : window
       context.fn = this
       var result = context.fn(...args)
       delete context.fn
       return result
     }

     Aa.hobby.myApply({
       name: 'huhu',
       age: 9
     }, [1, 2, 3])
```

## Bind

```js
    // 手写bind
    Function.prototype.myBind = function (context, ...args) {
      const fn = this
      args = args ? args : window
      return function newFn(...newFnArgs) {
        // 返回新的函数,要考虑到使用new去调用,并且new的优先级比较高,所以需要判断new的调用
        // if (this instanceof newFn) {
        //   return new fn(...args, ...newFnArgs)
        // }
        return fn.apply(context, [...args, ...newFnArgs])
      }
    }

    Aa.hobby.myBind({
      name: 'feifei',
      age: 28
    }, 1, 3, 4)()
```


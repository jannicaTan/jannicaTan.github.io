---
title: 关于配置hexo的坑及解决办法
date: 2021-12-27 09:52:38
tags: Hexo
categories: Hexo
---

最近在学习配置hexo，遇到了一些安装坑，去搜解决方式还遇到了网上不负责任的回答。于是决定还是记录下来 再有人和我一样的情况也不用抓耳挠腮了 

本文只针对**我遇到的问题和解决方式** 如有不对还请指出 

#### 环境及主题：

我使用的hexo+Github的配合

主题:keep主题,很推荐 整个的配置教程很清晰

这里放上github地址：`https://github.com/XPoet/hexo-theme-keep`

#### 1.关于指令：

`keep g`: 生成文件

`keep deploy`: 部署文件

`keep s`:可以在本地预览修改后的样子 

在正式提交前 可以在本地预览到满意再提交！不用一遍遍的提交去线上查看！！

#### 2.关于修改背景图片，部署到线上后，显示空白

首先打开开发者模式，在控制台查看是否图片报错，如果报错，多半是url出问题了,返回<u>主题的配置文件</u>中修改你的url就可以了

#### 3.关于keep主题分类/标签创建后，不能正确显示分类及个数

##### 3.1生成“分类”页并添加tpye属性

打开命令行，进入博客所在文件夹。执行命令

```cpp
$ hexo new page categories
```

找到`source/categories/index.md`这个文件，添加`type: "categories"`到内容中：

```css
---
title: category //这里注意一定要与themes/keep/layout/page.ejs中的关于分类的title一致
date: 2021-12-21 18:07:36
type: "categories"
---
```

保存并关闭文件。

❗️关于不能正确显示分类及个数检查两点❗️

- keep主题：
  - 检查这里的title名是否与`themes/keep/layout/page.ejs`中的关于分类的title一致：应为category或者categories
- 非keep主题:
  - 找到主题对应的`themes/keep/layout/`再其下方文件中找到关于分类的`xxx.ejs`文件复制文件名，返回`source/categories/index.md`添加一行`layout: xxx.ejs`即可

##### 3.2 给文章添加“categories”属性

打开需要添加分类的文章，为其添加categories属性。下方的`categories: web前端`表示添加这篇文章到“web前端”这个分类。注意：hexo一篇文章只能属于一个分类，也就是说如果在“- web前端”下方添加“-xxx”，hexo不会产生两个分类，而是把分类嵌套（即该文章属于 “- web前端”下的 “-xxx ”分类）。

```css
---
title: 文章标题
date: XXXXX
categories: 文章对应的分类（自拟）
---
```

⚠️注意：只有添加了`categories: xxx`的文章才会被收录到首页的“分类”中。

#### 4.关于hexo多终端同步的问题

我找到两个方法，目前我使用的是第一种，这两种方法的解答都将多终端解释的比较清楚，可以自行选择

- https://www.jianshu.com/p/fceaf373d797
- https://www.zhihu.com/question/21193762
  - 直上云霄的回答
  - http://fangzh.top/2018/2018090715/

#### 5.未待完续


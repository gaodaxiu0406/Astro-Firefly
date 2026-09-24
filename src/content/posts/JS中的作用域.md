---
# 必填。项目名称。
title: "JS中的作用域"
# 可选，和文章一样使用。
slug: JS中的作用域
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-04-29
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "JS中的作用域"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Javascript
tags:
  - Javascript
  - JS
  - 作用域
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

#### 1.内存

1. 堆内存：来存储东西的，一般来存储引用数据类型

2. 栈内存：代码执行空间，作用域

<!-- more -->
#### 2.作用域(两种)

1. 全局作用域：一打开浏览器就会形成
2. 私有作用域：函数执行形成的作用域

#### 3.函数执行的时候

1. 函数一执行，形成一个私有作用域
2. 有形参数的话给形参数赋值，相当于 `var` 一个变量，`function s(a){}`,`s(1)` -> `var a=1`;
3. 预解释
4. 代码执行

#### 4.私有变量(两种)

1. 形参
2. 在私有作用域中声明的变量，`var`过和`function`过得

**记住：私有变量只能私有作用域自己使用，别人获取不到**

#### 5.闭包

函数执行的时候形参一个私有作用域，来保护里面的私有变量不受外界干扰，这种机制叫做闭包。

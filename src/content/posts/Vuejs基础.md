---
# 必填。项目名称。
title: "Vuejs基础"
# 可选，和文章一样使用。
# slug: Vuejs基础
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2018-08-26
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "Vuejs基础"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
image: ""
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
tags:
  - vue
---

## Vue.js是什么

- Vue.js（读音 /vjuː/，类似于 view） 是一套构建用户界面的**渐进式框架**。
- 与其他重量级框架不同的是，Vue 采用自底向上增量开发的设计。Vue 的核心库只关注视图层，它不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与单文件组件和 Vue 生态系统支持的库结合使用时，Vue 也完全能够为复杂的单页应用程序提供驱动。
<!-- more -->
## vue的特点

- 核心只关注视图层(view)
- 易学，轻量，灵活
- 适用于移动端项目
- 渐进式框架

## 框架和库

- 框架 (vue的核心是库，但是我们用的时候，用的就是他的框架了)
    >总结:拥有完整的解决方案，我们写好，人家调用我（被动）

- 库
  - jquery
  - underscore模板库(模板引擎)
  - zepto
  - animate.css动画库

- 总结:
- 共同点:要用的时候 直接调用一下即可
- 人家写好，我们调用他（主动）

## 渐进式(渐进增强:低版本不支持，做成支持的，让高版本的更炫更支持)

- vue全家桶
  - 核心:vuejs
  - vue-router 可以帮我们实现一个单页应用
  - vuex 状态管理，可以帮我们完成组件化开发
  - axios 用来获取数据的
- 通过组合完成一个完整的框架

> 渐进式的理解
- 声明式渲染(无需关心如何实现)
- 组件系统
- 客户端路由(vue-router)
- 大规模状态管理(vuex)
- 构建工具(vue-cli)

## vue的两个核心点

- 响应的数据变化
  - 当数据发生改变->视图自动更新

- 组合的视图组件
  - ui页面映射为组件树
  - 划分组件可维护、可复用、可测试

## MVVM模式:双向绑定(angular、vue框架)

- M:model数据
- V:view视图
- viewModel视图模型

## MVC模式:单向(backbone框架)

- M:model数据
- V:view视图
- C:controller控制器

## vue优点

- 数据驱动(主要操作的是数据,几乎不直接操作dom)

## 如何安装vue

- 1. 通过bower
安装bower: `npm install bower -g`
mac本: `sudo npm install bower -g`
查看vue的版本 ： `bower info vue`
安装vue：`bower install vue@1.0.28`

- 2. 通过npm安装
通过npm: `npm install vue`
通过npm全局安装: `npm install vue -g`

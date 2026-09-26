---
# 必填。项目名称。
title: "Vue 的响应式原理中 Object.defineProperty 有什么缺陷？为什么在 Vue3.0 采用了 Proxy？"
# 可选，和文章一样使用。
slug: Object.defineProperty与Proxy
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2020-10-12
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "Vue 的响应式原理中 `Object.defineProperty` 有什么缺陷？为什么在 Vue3.0 采用了 `Proxy`，抛弃了 `Object.defineProperty`？"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Vue
tags:
  - Proxy
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

### Vue 的响应式原理中 `Object.defineProperty` 有什么缺陷？为什么在 Vue3.0 采用了 `Proxy`，抛弃了 `Object.defineProperty`？

#### `Object.defineProperty`

1) `Object.defineProperty` 无法低耗费的监听到数组下标的变化，导致通过数组下标添加元素，不能实时响应；
2) `Object.defineProperty` 只能劫持对象的属性，从而需要对每个对象，每个属性进行遍历。如果属性值是对象，还需要深度遍历。

#### `Proxy`

1) `Proxy` 可以劫持整个对象， 并返回一个新的对象。
2) `Proxy` 不仅可以代理对象，还可以代理数组。还可以代理动态增加的属性。

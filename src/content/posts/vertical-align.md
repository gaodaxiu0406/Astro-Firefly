---
# 必填。项目名称。
title: "vertical-align"
# 可选，和文章一样使用。
slug: css基础,vertical-align
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-09-01
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "css基础,vertical-align"
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
  - css
  - vertical-align
---

## vertical-align

- 改变基线对齐方式
  - vertical-align: top; 顶部对齐
  - vertical-align: bottom; 底部对齐
  - vertical-align: middle; 中部对齐

<!-- more -->
|值|描述|
|----|----|
|长度|通过距离升高（正值）或降低（负值）元素。'0cm'等同于'baseline'|
|百分值 – %|通过距离（相对于1line-height1值的百分大小）升高（正值）或降低（负值）元素。'0%'等同于'baseline'|
|baseline|默认。当前元素的基线与父元素的基线对齐。|
|sub|降低元素的基线到父元素合适的下标位置。|
|super|升高元素的基线到父元素合适的上标位置。|
|top|所有平级元素,去找最高(高度最高)元素的顶部进行对齐|
|text-top|把元素的顶端与父元素内容区域的顶端对齐。|
|middle|所有平级元素,去找最高(高度最高)元素的中部进行对齐|
|bottom|所有平级元素,去找最高(高度最高)元素的底部进行对齐|
|text-bottom|把元素的底端与父元素内容区域的底端对齐。|
|inherit|采用父元素相关属性的相同的指定值|

## 浏览器支持

- 所有浏览器都支持 vertical-align 属性。
- **注释：任何的版本的 Internet Explorer （包括 IE8）都不支持属性值 "inherit"。**

> 深入理解line-height与vertical-align推荐地址:[http://www.cnblogs.com/xiaohuochai/p/5271217.html](http://www.cnblogs.com/xiaohuochai/p/5271217.html)
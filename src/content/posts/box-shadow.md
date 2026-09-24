---
# 必填。项目名称。
title: "box-shadow和text-shadow"
# 可选，和文章一样使用。
slug: box-shadow和text-shadow
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-08-20
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "box-shadow和text-shadow"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: CSS
tags:
  - CSS
  - box-shadow
  - text-shadow
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
## box-shadow 属性向框添加一个或多个阴影
- 相关小项目地址:https://github.com/gaodaxiu0406/HEXOcase(CSS/小项目练习)
<!-- more -->
### 语法
#### CSS语法
```
box-shadow: h-shadow v-shadow blur spread color inset;
```
##### 注释
- box-shadow 向框添加一个或多个阴影。该属性是由逗号分隔的阴影列表，每个阴影由 2-4 个长度值、可选的颜色值以及可选的 inset 关键词来规定。省略长度的值是 0。

|值|描述|
|----|----|
|h-shadow|必需。水平阴影的位置。允许负值。|
|v-shadow|必需。垂直阴影的位置。允许负值。|
|blur|可选。模糊距离。|
|spread|可选。阴影的尺寸。|
|color|可选。阴影的颜色。请参阅 CSS 颜色值。|
|inset|可选。将外部阴影 (outset) 改为内部阴影。|

```
box-shadow: 10px 20px 30px 40px #000 inset;
```

#### JavaScript语法
```
object.style.boxShadow="10px 10px 5px #888888"
```

## text-shadow

### 语法
#### CSS语法
```
text-shadow: h-shadow v-shadow blur color;
```
##### 注释
- text-shadow 属性向文本添加一个或多个阴影。该属性是逗号分隔的阴影列表，每个阴影有两个或三个长度值和一个可选的颜色值进行规定。省略的长度是 0。

|值|描述|
|----|----|
|h-shadow|必需。水平阴影的位置。允许负值。|
|v-shadow|必需。垂直阴影的位置。允许负值。|
|blur|可选。模糊的距离。|
|color|可选。阴影的颜色。参阅 CSS 颜色值。|

```
text-shadow: 10px 20px 30px #000;
```

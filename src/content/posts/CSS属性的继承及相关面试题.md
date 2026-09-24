---
# 必填。项目名称。
title: "CSS属性的继承及相关面试题"
# 可选，和文章一样使用。
slug: CSS属性的继承及相关面试题
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-30
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "CSS属性的继承及相关面试题"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: CSS
tags:
  - CSS
  - CSS面试题
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
## CSS属性的继承
- 子级元素从父级元素身上继承的一些可继承的css属性
<!-- more -->
```html
<style>
div{color:red;}
</style>
<p>woshiyige[biaoqian</p>
```
- 根据 CSS，子元素从父元素继承属性。看看下面这条规则：
    - body {font-family: Verdana, sans-serif;}
        - 根据上面这条规则，站点的 body 元素将使用 Verdana 字体（假如访问者的系统中存在该字体的话）。
- 继承的权重较小，可被其他选择器的样式覆盖


## 面试题：
- 哪些css样式可以被继承：和文字有关的css样式 和列表有关的css样式
### 总结：
- 1.可继承属性
- 1)可以继承的文本相关属性：
```html
<azimuth><border-collapse><border-spacing><caption-side><color><cursor><direction><elevation><empty-cells><font-family><font-size><font-style><font-variant><font-weight><font><letter-spacing><line-height><list-style-image><list-style-position><list-style-type><list-style><orphans><pitch-range><pitch><quotes><richness><speak-header><speaknumeral><speak-punctuation><speak><speechrate><stress><text-align><text-indent><texttransform><visibility><voice-family><volume><whitespace><widows><word-spacing>
```
- 2)可以继承的列表相关属性：
```html
<azimuth><border-collapse><border-spacing><caption-side><color><cursor><direction><elevation><empty-cells><font-family><font-size><font-style><font-variant><font-weight><font><letter-spacing><line-height><list-style-image><list-style-position><list-style-type><list-style><orphans><pitch-range><pitch><quotes><richness><speak-header><speaknumeral><speak-punctuation><speak><speechrate><stress><text-align><text-indent><texttransform><visibility><voice-family><volume><whitespace><widows><word-spacing>
```
- 2.不可继承属性
```html
<display><margin><border><padding><background><height><min-height><max-height><width><min-width><max-width><overflow><position><left><right><top><bottom><z-index><float><clear><table-layout><vertical-align><page-break-after><page-bread-before>和<unicode-bidi>
```
- 3.所有元素可继承：
- `<visibility>（可见性）和<cursor>(光标)`

- 4.终端块状元素可继承：
- `<text-indent>和<text-align>`


- 5.如果css属性不带有继承性，如何继承父级身上的属性，可以将要继承的属性的属性值写上inherit
```css
ul{float:left;}
li{float:inherit;}
```
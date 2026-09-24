---
# 必填。项目名称。
title: "CSS中的display"
# 可选，和文章一样使用。
slug: CSS中的display
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-08-20
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "CSS中的display"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: CSS
tags:
  - CSS
  - display
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
- 根据这个属性可以将元素分成不同的类型,也会显示出不同的状态,例如属性值为block的时候,这个元素会独占一行,如果属性值为inline的时候,所有这个属性值得元素都会在一行显示,属性值为none,元素会在页面上消失.
- 所有元素都有天生自带的display属性和属性值,叫做内置属性
<!-- more -->
## display:block; 块级元素(块状元素)
>　特点:
- 独占一行,在所在父元素内依次向下排列,从左上角开始
- 宽度在不设置的情况下,宽度继承父级元素内容的宽,高度由本身内容决定
- 可以直接设置盒子模型的所有属性(width,height,padding,border,margin)
- 可以嵌套其他元素(p,dt,h1-h6不能嵌套块级)
    - dt/p 不能嵌套其他块级元素,可以嵌套行内元素等
- 永远会在父级盒子的左上角开始排布,从上到下排.

> 人为设置的样式要比自带的样式权重高
> 块级元素这些特点,我们将其称作**BFC(Block Fomatting Context**-->块级盒子在上下文中的渲染模式)

## display:inline; 行内元素
>　特点:
- 在一行显示
- 不能设置宽度 高度
- padding margin的上下值设置不生效,左右值生效
- 默认宽度高度是本身内容的宽高
- 几个行内元素默认的垂直方向的对齐方式是基线对齐
- 在编辑代码时,如果行内元素之间有**回车或者空格**,那么在页面显示的时候,就会默认有间隙()
   - **将父级的font-size设置为0,可以解决这个问题**.
- **行内元素不能嵌套块级元素**

## display:inline-block; 行内块级元素
> 特点:
- 在一行显示
- 可以直接设置宽度高度padding、margin值
- 默认宽度高度是本身内容的宽高
- 几个行内元素默认的垂直方向对齐方式是基线对齐
- 在编辑代码时,如果行内元素之间有回车或者空格,那么在页面显示的时候,就会默认有间隙
   - 将父级的font-size设置为0,可以解决这个问题.
- 行内元素不能嵌套块级元素

## vertical-align改变行内元素和行内块级元素的基线对其方式

|||
|----|----|
|top|所有平级元素,去找最高(高度最高)元素的顶部进行对齐|
|bottom|所有平级元素,去找最高(高度最高)元素的底部进行对齐|
|middle|所有平级元素,去找最高(高度最高)元素的中部进行对齐|
|length(数值)|px 或 %|

>　改变对齐方式的时候,所有元素都要添加vertical-align这个属性

## display:none; 将这个元素在页面上隐藏起来
> 如何再让设置display:none;的元素显示出来?
- 将none用其他的属性替换
    - 例如:重新设置display属性为==>display:block;


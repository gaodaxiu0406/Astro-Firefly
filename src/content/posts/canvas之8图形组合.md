---
# 必填。项目名称。
title: "Canvas之8图形组合"
# 可选，和文章一样使用。
slug: Canvas之8图形组合
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-09
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "Canvas之8图形组合"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: CSS
tags:
  - Canvas
  - CSS
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
#### 图形组合
- cvs.globalCompositeOperation=type;
- type的值:
    - 1.source-over 默认值 覆盖 在原来的图形上绘制新图 新图在上
    - 2.source-out 显示新图的非交集部分
    - 3.source-in 显示新图和图形的交集，颜色是新图的颜色
    - 4.source-atop 显示旧图和交集部分 交集是新图颜色
    - 5.destination-over  在原来图形的下面绘制新图 旧图在上
    - 6.destination-out 显示旧图的非交集部分
    - 7.destination-in 显示交集 颜色是旧图颜色
    - 8.destination-atop 显示新图和交集部分 交集是旧图颜色
    - 9.lighter:全部显示 交集部分是叠加颜色
    - 10.xor:显示新旧图的非交集部分
    - 11.copy 只显示新图
<!-- more -->
- 案例1:在原来的图形上绘制新图 新图在上
```js
	var draw=document.getElementById('draw');
	var cvs=draw.getContext('2d');
	function draw1(){
		cvs.fillStyle='gold';
		cvs.fillRect(10,10,100,100);
        cvs.globalCompositeOperation='source-over';
		cvs.fillStyle='pink';
		cvs.fillRect(50,50,100,100);
	}
	draw1();
```
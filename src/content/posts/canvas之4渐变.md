---
# 必填。项目名称。
title: "Canvas之4渐变"
# 可选，和文章一样使用。
slug: Canvas之4渐变
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-09
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "Canvas之4渐变"
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
- 1.线性渐变
- var CLG=cvs.createLinearGradient(x0,y0,x1,y1);
    - x0:渐变开始的x坐标
    - y0:渐变开始的y坐标
    - x1:渐变结束的x坐标
    - y1:渐变结束的y坐标
- CLG.addColorStop(n,m);
    - n:设置颜色的偏移量
    - m:颜色
<!-- more -->
- 例如:

```js
function draw1(){
	var CLG=cvs.createLinearGradient(0,0,200,200);
	//创建一个线性渐变 渐变开始的坐标0,0 渐变结束的坐标200,200 (即从左上角到右下角渐变)
	CLG.addColorStop(0,'red');//设置渐变的偏移量0% 颜色红色
	CLG.addColorStop(0.25,'yellow');//设置渐变的偏移量25% 颜色黄色
	CLG.addColorStop(0.5,'skyblue');//设置渐变的偏移量50% 颜色天空蓝
	CLG.addColorStop(0.75,'orange');//设置渐变的偏移量75% 颜色橘黄
	CLG.addColorStop(1,'pink');//设置渐变的偏移量100% 颜色粉色
	cvs.fillStyle=CLG;//设置填充样式是线性渐变
	cvs.fillRect(0,0,200,200);//设置填充矩形 左上角坐标0,0  宽200px  高200px
	cvs.fill();//设置样式为填充样式
}
draw1();
```

- 2.径向渐变(发散性渐变)
- cvs.createRadialGradient(x0,y0,x1,y1,r1);
    - x0:发散渐变开始中心的x坐标
    - y0：发散渐变开始中心的y坐标
    - r0:发散渐变开始的半径
    - x1:发散渐变结束中心的x坐标
    - y1：发散渐变结束中心的y坐标
    - r1:发散渐变结束的半径
- 例如:

```js
function draw2(){
	var CRG=cvs.createRadialGradient(200,200,200,200,200,10);
	//创建一个径向/发散性渐变 渐变开始的坐标200,200 渐变开始的半径200px 渐变结束的坐标200,200 渐变结束的半径10px
	CRG.addColorStop(0,'purple');
	CRG.addColorStop(0.2,'yellow');
	CRG.addColorStop(0.4,'pink');
	CRG.addColorStop(0.6,'lightblue');
	CRG.addColorStop(0.8,'skyblue');
	CRG.addColorStop(1,'white');
	cvs.fillStyle=CRG;//设置填充样式是径向渐变
	cvs.fillRect(100,100,200,200);
	//设置填充矩形 左上角坐标100,100  宽200px  高200px
}
draw2();
```

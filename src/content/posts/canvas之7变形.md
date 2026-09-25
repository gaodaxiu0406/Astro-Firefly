---
# 必填。项目名称。
title: "Canvas之7变形"
# 可选，和文章一样使用。
slug: Canvas之7变形
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-09
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "Canvas之7变形"
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
- 1. 平移translate(x,y);
x:坐标原点向x轴平移的距离
y:坐标原点向y轴平移的距离

<!-- more -->
- 案例

```js
	function draw1(){
		cvs.fillStyle='skyblue';
		//设置填充颜色天空蓝
		cvs.fillRect(0,0,200,100);
		//矩形左上角坐标0,0 宽200px 高100px
		cvs.translate(50,50);
		//设置平移 坐标原点向x轴(向右)平移50px 坐标原点向y轴(向下)偏移50px
		//-->这个平移只会对后面的矩形造成影响 不会影响前面的
		cvs.fillStyle='pink';
		//设置填充颜色粉色
		cvs.fillRect(0,0,180,80);
		//矩形左上角坐标0,0 宽180px 高80px
	}
	draw1();
```

- 2. 缩放 vas.scale(x0,y0);
x0:x轴按照x0的比例缩放
y0:y轴按照x0的比例缩放

- 案例

```js
	function draw2(){
		cvs.scale(1,2);//设置缩放 x轴不变 y轴是之前的2倍
		cvs.fillStyle='plum';//设置填充样式为颜色填充
		cvs.fillRect(0,0,200,100);
		//矩形左上角坐标0,0 宽200px 高100px
		//-->那么转化后的矩形宽200px 高200px
	}
	draw2();
```

- 3.旋转 vas.rotate(angle);
angle:坐标轴转的角度 他是一个弧度(和画圆的计算是一样的)

- 案例

```js
	function draw3(){
		cvs.rotate(Math.PI/4);//设置旋转  旋转角度为45度
		cvs.fillStyle='lightblue';
		cvs.fillRect(100,100,200,100);
	}
	draw3();
```

> 注意：平移、缩放、旋转都是对原始坐标（画布）操作的

-  例如:

```js
function draw3(){
	cvs.translate(200,0);//此时的原点已经变到200,0的位置
	cvs.rotate(Math.PI/4);//设置旋转  旋转角度为45度
	cvs.fillStyle='lightblue';
	cvs.fillRect(100,100,200,100);
}
draw3();
```

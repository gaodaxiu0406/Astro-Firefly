---
# 必填。项目名称。
title: "Canvas之1绘制线条的有关属性和步骤"
# 可选，和文章一样使用。
slug: Canvas之1绘制线条的有关属性和步骤
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-08
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "Canvas之1绘制线条的有关属性和步骤"
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
`<canvas id="" width="" height=""></canvas>`
canvas :H5标签 在页面上绘制图形用的（通常称他画布）
canvas只是一个容器，我们用js脚本来控制他
`<canvas id="draw" width="600" height="500" style="border: 1px solid #ccc;"></canvas>`

<!-- more -->
### 绘制线条的有关属性和步骤

> 1.相关属性

- 1.填充的样式
  - `cvs.fillStyle --> `fillStyle`填充样式
  - `cvs.strokeStyle --> `strokeStyle`笔触样式 主要用来画边框的`
  - `cvs.lineWidth --> 边框的宽度`

- 2.绘制图形有两种方式
  - `cvs.fill(); --> 填充样式`
  - `cvs.stroke(); --> 边框样式`

- 3.颜色值的四种书写方式
  - 1).颜色名      -->"red"
  - 2).十六进制    -->"#fff"
  - 3).三色值      -->rgb(0,0,0)
  - 4).四色值      -->rgba(0,0,0,0.3)

- 4.坐标:
  - 1.)以画布为基准,距离画布的上边是y坐标值(top值),距离画布的左边是x坐标值(left值);
  - cvs.moveTo(x,y);  --> 起始点坐标
  - cvs.lineTo(x,y);  --> 结束点的坐标
  - 如果没有moveTo就把上一个挨着的lineTo作为起始坐标
  - 例如:假如第一个不是moveTo而是lineTo,那么lineTo就是其实坐标
- 5.开始和关闭一个路径
  - cvs.beginPath(); --> 开始一个新的路径
  - cvs.closePath(); --> 关闭当前路径
  - 注意:加上.closePath会自动闭合 会自动连接起始坐标和结束坐标

- 6.canvas中的圆角
  - 1).设置线条交汇处的样式
  - cvs.lineJoin 他有三个属性：
    - 1).尖角miter
    - 2).斜角bevel
    - 3).圆角round
  - 2).设置一条线段两端点的样式
  - lineCap焦点样式
    - 1)平的butt(默认值)
    - 2.)圆角round
    - 3.)方角square

> 2.步骤及案例

- 步骤1.获取出canvas标签,例如:
`var draw=document.getElementById('draw');`

- 步骤2.设置绘制环境--2d 平面图,例如:

```js
var cvs=draw.getContext('2d');
//cvs 这个就是你的画板 接下来就可以在cvs上进行绘制

```

- 步骤3
- 案例1:线段

```js
	function draw1(){
	var draw=document.getElementById('draw');
	var cvs=draw.getContext('2d');
	cvs.beginPath();
	cvs.moveTo(50,50);
	cvs.lineTo(150,50);
	cvs.closePath();
	cvs.strokeStyle='#800080';
	cvs.lineWidth=5;
	cvs.stroke();//以边框的形式显示
	}
	draw1();
```

- 案例2:等腰直角三角形

```js
function draw2(){
	var draw=document.getElementById('draw');
	var cvs=draw.getContext('2d');
	cvs.beginPath();
	cvs.lineTo(80,120);
	cvs.lineTo(80,240);
	cvs.lineTo(200,240);
	cvs.closePath();
	cvs.strokeStyle='ec568c';
	cvs.lineWidth=10;
	cvs.stroke();
}
draw2();
```

- 案例3:圆角矩形

```js
function draw3(){
	var draw=document.getElementById('draw');
	var cvs=draw.getContext('2d');
	cvs.beginPath();
	cvs.lineCap='round';
	cvs.lineTo(50,50);
	cvs.lineTo(250,50);
	cvs.closePath();//关闭就没有圆角效果
	cvs.lineWidth=100;
	cvs.strokeStyle='#896446';
	cvs.stroke();
}
draw3();
```

- 案例4:圆角三角形

```js
function draw4(){
	var draw=document.getElementById('draw');
	var cvs=draw.getContext('2d');
	cvs.beginPath();
	cvs.lineJoin='round';//设置圆角
	cvs.moveTo(200,100);
	cvs.lineTo(100,250);
	cvs.lineTo(300,250);
	cvs.closePath();
	cvs.lineWidth=50;
	cvs.strokeStyle='#896446';
	cvs.stroke();
}
draw4();
```

---
# 必填。项目名称。
title: "Canvas之2画圆"
# 可选，和文章一样使用。
slug: Canvas之2画圆
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-08
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "Canvas之2画圆"
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
- 1. cvs.arc(x,y,radius,startAngle,endAngle,anticlokwise);
  - x,y 圆心坐标
  - radius半径r
  - startAngle 起始角 以弧度计算(钟表的3点钟方向是0度,也就是x轴的正方向是0度,默认是顺时针)
  - endAngle  结束角
  - anticlokwise 是否逆时针 默认值false false表示顺时针
<!-- more -->
- 2. 案例

案例1:边框半圆

```js
	function draw1(){//边框圆
		cvs.strokeStyle='#ffa50';//设置笔触样式(边框样式)颜色
		cvs.beginPath();//开始一个路径
		cvs.arc(500,500,100,0,Math.PI);//圆心坐标是500,500，半径是100px，起始角为0度，结束角为180度
		cvs.closePath();//结束路径
		cvs.lineWidth=10;//边框宽度为10px
		cvs.stroke();//绘制图形以边框样式绘制
	}
	draw1();
```

案例2:同心圆

```js
function draw2(){
	cvs.fillStyle='orange';
	cvs.beginPath();
	//开始一个新的路径
	cvs.arc(200,200,60,Math.PI/2,2*Math.PI);
	//圆心坐标是(200,200),半径为60px,起始角为90度,结束角为360度
	cvs.closePath();
	//结束一个路径
	cvs.fill();
	//绘制图形以填充样式绘制
	cvs.strokeStyle='yellow';
	//设置 笔触样式(边框样式) 为黄色
	cvs.lineWidth=40;
	//边框的宽度为40px
	cvs.beginPath();
	//开始一个新的路径
	cvs.arc(200,200,80,0,2*Math.PI);
	//圆心坐标是(200,200),半径为80px,起始角度为0度,结束角度为360度
	cvs.closePath();//结束一个路径
	cvs.stroke();//绘制图形以边框样式绘制
}
draw2();
```

案例3:每次调用fill绘制填充图的时候，会把当次路径的起始点和结束点分别连接，填充闭合部分(如果想让每个路径互不干扰 一定要记得写结束路径-->关闭路径)

```js
function draw3(){
	cvs.strokeStyle='pink';//设置笔触样式(边框样式)颜色为粉色
	cvs.beginPath();//开始一个路径
	cvs.lineWidth=2;//边框的宽度为2px
	cvs.arc(100,100,100,0,Math.PI);//圆心坐标是100,100,半径为100,起始角度为0度,结束角度为180度
	cvs.closePath();//结束一个路径
	cvs.stroke();//绘制图形以边框样式绘制
	cvs.fillStyle='gray';//设置填充颜色为灰色
	cvs.arc(300,300,80,0,Math.PI/2);//圆心坐标是300,300，半径是80px，起始角度为0，结束角度为90度
	cvs.closePath();
	cvs.fill();
}
draw3();
```

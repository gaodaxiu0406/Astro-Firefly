---
# 必填。项目名称。
title: "Canvas之3绘制矩形"
# 可选，和文章一样使用。
slug: Canvas之3绘制矩形
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-09
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "Canvas之3绘制矩形"
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
- 1. cvs.fillRect(x,y,w,h); --> 填充矩形
    - x,y 是这个矩形左上角的坐标
    - w,h 是这个矩形的宽高
<!-- more -->
- 2. cvs.strokeRect(x,y,w,h); --> 带边框的矩形
    - x,y 是这个矩形左上角的坐标
    - w,h 是这个矩形的宽高
        - 注意:如果设置边框 边框一半在里面一半在外面
- 3. cvs.clearRect(x,y,w,h); --> 清除填充图的某一部分，清除的还是一个矩形
    - x,y 是这个矩形左上角的坐标
    - w,h 是这个矩形的宽高
##### 案例
- 案例1
```js
	function draw1(){
		//填充矩形
		cvs.fillStyle='#fccdda';//画之前填充颜色
		cvs.fillRect(10,20,100,50);//设置填充矩形,矩形的左上角坐标为10,20 宽100px 高50px
		//边框矩形
		cvs.strokeStyle='red';//设置边框的矩形边框颜色
		cvs.lineWidth=20;//设置边框宽度20px
		cvs.strokeRect(150,20,100,50);//设置边框矩形，	矩形的左上角坐标为150,20 宽100px 高50px
	}
	draw1();
```
- 案例2
```js
function draw2(){//清除填充图的某一部分，清除的还是一个矩形cvs.clearRect(x,y,w,h)
	cvs.fillStyle='orange';
	//画之前填充颜色
	cvs.fillRect(20,100,300,100);
	//设置填充矩形,矩形左上角坐标为20,100 宽300px 高100px
	cvs.clearRect(140,140,60,60);
	//清除填充图的矩形 清除的这个矩形左上角坐标140,140 宽60px 高60px
	cvs.clearRect(20,100,40,40);
	//清除填充图的矩形 清除的这个矩形左上角坐标20,100 宽40px 高40px
	cvs.clearRect(280,100,40,40);
	//清除填充图的矩形 清除的这个矩形左上角坐标280,100 宽40px 高40px
}
draw2();
```

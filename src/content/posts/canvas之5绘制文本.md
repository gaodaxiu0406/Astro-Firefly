---
# 必填。项目名称。
title: "Canvas之5绘制文本"
# 可选，和文章一样使用。
slug: Canvas之5绘制文本
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-09
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "Canvas之5绘制文本"
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
- 1.阴影
    - cvs.shadowOffsetX//阴影的横向偏移量，默认值是0
    - cvs.shadowOffsetY//阴影的纵向偏移量，默认值是0
    - cvs.shadowColor//阴影的颜色
    - cvs.shadowBlur//阴影的模糊范围（值越大越模糊）
<!-- more -->
- 案例
```
	function draw1(){
		cvs.shadowColor='#000fff';//设置阴影颜色
		cvs.shadowOffsetX=30;//设置阴影的横向偏移量30px
		cvs.shadowOffsetY=20;//设置阴影的纵向偏移量20px
		cvs.shadowBlur=20;//设置阴影的模糊范围20px
		cvs.fillStyle='#449fdb';//设置填充的样式为颜色填充
		cvs.fillRect(50,50,100,100);//设置填充矩形 左上角坐标50,50 宽100px 高100px
	}
	draw1();
```
- 2.绘制文本
    - 设置字体样式 cvs.font='字体大小font-size 字体样式font-family'
    - 水平对齐方式 cvs.textAlign(start,end,right,center);
    - 垂直对齐方式 cvs.textBaseline=''
    - 属性值:top,middle,hangle,bottom,alphabetic,ideographic
    - 计算文本长度
        - var text='dfbzbh'
        - console.log(cvs.measureText(text));//width:40.453125
    - 填充文字
        - cvs.fillText(text,x,y,maxWidth);
        - 1) text:文本内容
        - 2) x:文字起始点的横坐标
        - 3) y:文字起始点的纵坐标
    - 绘制文字轮廓
        - cvs.strokeText(text,x,y,maxWidth);
        - 1) text:文本内容
        - 2) x:文字起始点的横坐标
        - 3) y:文字起始点的纵坐标

- 案例1
```js
function draw1(){
		cvs.shadowColor='#000fff';//设置阴影颜色
		cvs.shadowOffsetX=30;//设置阴影的横向偏移量30px
		cvs.shadowOffsetY=20;//设置阴影的纵向偏移量20px
		cvs.shadowBlur=20;//设置阴影的模糊范围20px
		cvs.fillStyle='#449fdb';//设置填充的样式为颜色填充
		cvs.fillRect(50,50,100,100);
		//设置填充矩形 左上角坐标50,50 宽100px 高100px
	}
	draw1();
```
- 案例2
```js
	function draw2(){
		var text='hellow word';//设置文本内容
		cvs.fillStyle='yellow';//设置填充样式颜色
		cvs.font='40px verdana';//设置字体样式
		cvs.textAlign='start';//设置字体的水平对齐方式
		cvs.textBaseline='top';//设置字体的垂直对齐方式
		cvs.fillText(text,10,10);
		//设置填充文字 文本内容text 文本起始点坐标10,10
		var length=cvs.measureText(text);
		//获取文本宽度(长度)length
		console.dir(length);
		//TextMetrics-->width:241.171875
		//==>length.width字体的宽度
		cvs.fillText("字体长度为"+length.width,10,60);
		//设置填充文字(通过字符串拼接方式) 文本起始点坐标10,60
	}
	draw2();
```
- 案例3:文本线性渐变
```js
function draw3(){
		var CLG=cvs.createLinearGradient(0,0,300,100);
		//创建一个线性渐变 渐变开始的坐标0,0 渐变结束的坐标300,100
		CLG.addColorStop(0,'skyblue');//设置渐变的偏移量0% 天空蓝
		CLG.addColorStop(0.25,'plum');//设置渐变的偏移量25% 紫色
		CLG.addColorStop(0.5,'lightblue');//设置渐变的偏移量50% 蓝
		CLG.addColorStop(0.75,'skyblue');//设置渐变的偏移量75% 天空蓝
		CLG.addColorStop(1,'plum');//设置渐变的偏移量100% 紫色
		var text='hellow word';//设置文本内容
		cvs.fillStyle=CLG;//设置填充样式是线性渐变
		cvs.shadowOffsetX=5;//设置阴影的横向偏移量5px
		cvs.shadowOffsetY=4;//设置阴影的纵向偏移量4px
		cvs.shadowColor='#ffb6c1';//设置阴影的颜色
		cvs.shadowBlur=5;//设置阴影的模糊度
		cvs.font='40px cursive';//设置字体样式
		cvs.textAlign='top';//设置字体的水平对齐方式
		cvs.fillText(text,50,150);
		//设置填充文字text 文本起始点坐标50,150
		var width=cvs.measureText(text).width;//获取文本宽度(长度)length
		cvs.fillText("字体长度为："+width,10,200);
		//设置填充文字(通过字符串拼接方式) 文本起始点坐标10,200

	}
	draw3();
```
- 案例4:文本径向渐变
```js
	function draw4(){
		var CRG=cvs.createLinearGradient(0,0,600,0,0,20);
		//创建一个径向渐变 渐变开始的坐标0,0 开始渐变的半径600px 渐变结束的坐标0,0 渐变结束的半径20px
		CRG.addColorStop(0,'pink');
		CRG.addColorStop(0.25,'skyblue');
		CRG.addColorStop(0.5,'yellow');
		CRG.addColorStop(0.75,'plum');
		CRG.addColorStop(1,'skyblue');
 		var text='I WANT EAT';
 		cvs.fillStyle=CRG;//设置填充样式是径向渐变
 		cvs.font='80px simsun';//设置字体样式
   		cvs.textAlign='start';//设置文本横向对齐方式
 		cvs.textBaseline='top';//设置文本纵向对齐方式
 		cvs.shadowColor='lightblue';//设置阴影颜色
 		cvs.shadowBlur=10;//设置阴影的模糊范围10px
 		cvs.fillText(text,10,10);//设置填充文字text 文本起始点坐标10,10
	}
	draw4();
```



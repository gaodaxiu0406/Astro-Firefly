---
# 必填。项目名称。
title: "Canvas之6绘制图片"
# 可选，和文章一样使用。
slug: Canvas之6绘制图片
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-09
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "Canvas之6绘制图片"
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
##### 绘图
- 1. cvs.drawImage(Image,x,y,w,h);
    - Image 就是可以放在DOM中的真实图片，可以动态创建，也可以获取页面上的
    - x,y 图片放入画布,在画布左上角的坐标
    - w,h 绘制图片的宽高
<!-- more -->
- 案例:将图片放在画布上
```js
	function draw1(){
		var img=new Image;//动态创建一个img
		img.src='default.gif';//添加图片链接
		img.onload=function(){//如果图片地址真实存在 执行这个函数
			cvs.drawImage(this,0,100,100,90);
			//将图片放在画布上 图片左上角的坐标0,100 图片宽100px 高90px
		}
	}
	draw1();
```

- 2. cvs.drawImage(img_elem,sx,sy,sw,sh,dx,dy,dw,dh);
    - sx,sy 图片左上角的坐标
    - sw,sh  矩形区域的宽高 用来截取图片
    - dx,dy  截取出来放在画布canvas上的坐标
    - dw,dh  画在canvas上的宽高

    - 总结:
        - sw,sy,sx,sy 是用来截取图片的过程
        - dx,dy,dw,dh 把截取出来的图片放在canvas上的过程

- 案例:截取图片
```js
	function draw2(){
		var img=new Image;//动态创建一个img
		img.src='1.jpg';//添加图片链接
		img.onload=function(){//如果图片地址真实存在 执行这个函数
			cvs.drawImage(this,480,150,440,410,0,0,200,200);
			//this就是img 将图片放在画布上 需要截取的图片在原图片左上角的坐标480,150  截取图片的大小为440px*410px 截取出来的图片放入画布的坐标0,0 截取出来的图片画在画布canvas的宽200px 高200px
		}
	}
//	draw2();
```

- 3. 设置平铺
- cvs.creatPattern(image,type)
    - Image 就是可以放在DOM中的真实图片，可以动态创建，也可以获取页面上的
    - type:
        - no-repeat 不平铺
        - repeat 全方向平铺
        - repeat-x x轴方向平铺
        - repeat-y y轴方向平铺

- 案例
```js
function draw3(){
	var img=new Image;
	img.src='default.gif';
	img.onload=function(){
		var rep=cvs.createPattern(this,'repeat');//设置图片平铺
		cvs.fillStyle=rep;//设置填充样式为图片平铺
		cvs.fillRect(0,0,draw.width,draw.height);
		//draw.width画布的宽 draw.height画布的高
		//设置填充矩形 矩形左上角坐标0,0 矩形的宽为画布的宽 矩形的高为画布的高
	}
}
//draw3();
```


---
# 必填。项目名称。
title: "Canvas动态案例"
# 可选，和文章一样使用。
slug: Canvas动态案例
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-09
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "Canvas动态案例"
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
- Canvas动态案例
<!-- more -->
```css
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
	</head>
	<body>
		<canvas id="draw" width="220" height="320" style="background-color: skyblue"></canvas>
	</body>
</html>
<script type="text/javascript">
	var draw=document.getElementById('draw');
	var cvs=draw.getContext('2d');
	var img=new Image;
	img.src='walkingdead.png';//添加图片地址
	img.onload=function(){//图片上有10张小图横着排列
		var width=this.width/10;
		var height=this.height;
		var i=0;
		window.setInterval(function(){
			cvs.clearRect(0,0,draw.width,draw.height);//清除上一个图片
		cvs.drawImage(img,i*width,0,width,height,0,0,width,height);
		if(i==9){
			i=0
		}else{i++;}
		},200);
	}
</script>
```
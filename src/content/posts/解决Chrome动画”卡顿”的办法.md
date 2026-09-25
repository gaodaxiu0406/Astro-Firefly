---
# 必填。项目名称。
title: "解决Chrome动画”卡顿”的办法"
# 可选，和文章一样使用。
slug: 解决Chrome动画”卡顿”的办法
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2018-08-31
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "解决Chrome动画”卡顿”的办法"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Css
tags:
  - Chrome动画”卡顿”
  - Css动画
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

解决Chrome动画”卡顿”的办法,为动画DOM元素添加CSS3样式
<!-- more -->
```css
-webkit-transform:transition3d(0,0,0);
//或
-webkit-transform:translateZ(0);
```

- 这两个属性都会开启GPU硬件加速模式，从而让览器在渲染动画时从CPU转向GPU;

- 其实说白了这是一个小伎俩，也可以算是一个Hack，-webkit-transform:transition3d和-webkit-transform:translateZ其实是为了渲染3D样式，但我们设置值为0后，并没有真正使用3D效果，但浏览器却因此开启了GPU硬件加速模式。

- 这种GPU硬件加速在当今PC机及移动设备上都已普及，在移动端的性能提升是相当显著地，所以建议大家在做动画时可以尝试一下开启GPU硬件加速。

- 当然也可以这样开启所有浏览器的GPU硬件加速：

```css
webkit-transform: translateZ(0);
-moz-transform: translateZ(0);
-ms-transform: translateZ(0);
-o-transform: translateZ(0);
transform: translateZ(0);
```

- 或者:

```css
webkit-transform: translate3d(0,0,0);
-moz-transform: translate3d(0,0,0);
-ms-transform: translate3d(0,0,0);
-o-transform: translate3d(0,0,0);
transform: translate3d(0,0,0);
```

- 使用`-webkit-transform:transition3d(0,0,0)`开启`GPU`硬件加速的`chrome`中渲染动画性能明显顺畅了许多

### chrome诡异的Bug

- 对所有动画DOM元素添加`-webkit-transform:transition3d(0,0,0)`开启GPU硬件加速之后，又出现了一个`chrome`诡异的Bug

- 当你有多个`position:absolute;`元素添加`-webkit-transform:transition3d(0,0,0);`开启`GPU`硬件加速之后，会有几个元素凭空消失

- 这可能是跟添加`-webkit-transform`之后`chrome`尝试使用`GPU`硬件加速有关系，最后还是要等待`Chrome`官方更新解决了，当前`Chrome`版本是33。如果谁发现比较好的解决办法，欢迎提出^_^

#### 如何避免这个问题

- 在使用`-webkit-transform`尝试对很多`DOM`元素编写3D动画时，尽量不要对这些元素及他们的父元素使用`position:absolute/fixed`。(其实这种情况很难避免)

- 临时解决办法是,减少使用`-webkit-transform:transition3d(0,0,0)`的`DOM`元素数量，例如从9个减至6个就没有元素消失的现象了。

### 开启GPU硬件加速可能触发的问题

- 通过`-webkit-transform:transition3d/translateZ`开启`GPU`硬件加速之后，有些时候可能会导致浏览器频繁闪烁或抖动，可以尝试以下办法解决之:

```css
-webkit-backface-visibility:hidden;
-webkit-perspective:1000;
```

### 如何监测动画帧速率

- 推荐两种实时监测网页渲染帧速率的方法：
  - 1.`Chrome`的`DevTool`中`TimeLine`的`Frame`模块
  - 2.地址栏输入”`chrome:flags`”搜索”`fps`”，将”FPS计数器”开启，浏览器重启后右上角会实时显示帧速率。

### 通过-webkit-transform:transition3d/translateZ开启GPU硬件加速的适用范围

- 使用很多大尺寸图片(尤其是`PNG24`图)进行动画的页面。
- 页面有很多大尺寸图片并且进行了`css`缩放处理，页面可以滚动时。
- 使用`background-size:cover`设置大尺寸背景图，并且页面可以滚动时。(详见:[https://coderwall.com/p/j5udlw](https://coderwall.com/p/j5udlw))
- 编写大量`DOM`元素进行`CSS3`动画时(`transition`/`transform`/`keyframes`/`absTop`&`Left`)
- 使用很多`PNG`图片拼接成`CSS Sprite`时

- **暂时只有这五种情况，欢迎大家补充**

#### 通过开启GPU硬件加速虽然可以提升动画渲染性能或解决一些棘手问题，但使用仍需谨慎，使用前一定要进行严谨的测试，否则它反而会大量占用浏览网页用户的系统资源，尤其是在移动端，肆无忌惮的开启GPU硬件加速会导致大量消耗设备电量，降低电池寿命等问题。

> 参考地址:[http://blog.bingo929.com/transform-translate3d-translatez-transition-gpu-hardware-acceleration.html](http://blog.bingo929.com/transform-translate3d-translatez-transition-gpu-hardware-acceleration.html)
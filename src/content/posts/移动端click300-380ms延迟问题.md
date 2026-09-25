---
# 必填。项目名称。
title: "移动端click300-380ms延迟问题"
# 可选，和文章一样使用。
slug: 移动端click300-380ms延迟问题
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-07-28
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "移动端click300-380ms延迟问题"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: CSS
tags:
  - CSS
  - 移动端
  - 移动端click延迟
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
# 移动设备上的web网页是有300ms延迟的，玩玩会造成按钮点击延迟甚至是点击失效。
<!-- more -->
## 历史原因

- 来源一个公司内一个同事的分享:2007年苹果发布首款iphone上iOS系统搭载的safari为了将适用于PC端上大屏幕的网页能比较好的展示在手机端上，使用了双击缩放(double tap to zoom)的方案，比如你在手机上用浏览器打开一个PC上的网页，你可能在看到页面内容虽然可以撑满整个屏幕，但是字体、图片都很小看不清，此时可以快速双击屏幕上的某一部分，你就能看清该部分放大后的内容，再次双击后能回到原始状态。 双击缩放是指用手指在屏幕上快速点击两次，ios 自带的 Safari 浏览器会将网页缩放至原始比例。 原因就出在浏览器需要如何判断快速点击上，当用户在屏幕上单击某一个元素时候，例如跳转链接，此处浏览器会先捕获该次单击，但浏览器不能决定用户是单纯要点击链接还是要双击该部分区域进行缩放操作，所以，捕获第一次单击后，浏览器会先Hold一段时间t，如果在t时间区间里用户未进行下一次点击，则浏览器会做单击跳转链接的处理，如果t时间里用户进行了第二次单击操作，则浏览器会禁止跳转，转而进行对该部分区域页面的缩放操作。那么这个时间区间t有多少呢？在IOS safari下，大概为300毫秒。这就是延迟的由来。造成的后果用户纯粹单击页面，页面需要过一段时间才响应，给用户慢体验感觉，对于web开发者来说是，页面js捕获click事件的回调函数处理，需要300ms后才生效，也就间接导致影响其他业务逻辑的处理。

## 解决方案

### 1.tap.js解决方案

- 使用 zepto.js 的 tap 事件，通过 singleTap 和 doubleTap 来区分单击和双击。但是会出现点击穿透，而且对于已经使用 click 的文件，改动成本太大。

```html
<script src="tap.js"></script>

<div id="container">
  <button id="button-1">Click event</button>
  <button id="button-2">Tap event</button>
</div>

<div id="output"></div>

<script>
  var container = document.getElementById('container')
  var button1 = document.getElementById('button-1');
  var button2 = document.getElementById('button-2');
  var output = document.getElementById('output');

  var tap = new Tap(container);

  button1.addEventListener('click', callback, false);
  button2.addEventListener('tap', callback, false);

  function callback (e) {
      e.preventDefault();
      var p = document.createElement('p');
      p.textContent = 'event: ' + e.type;
      output.insertBefore(p, output.firstChild);
  }
</script>
```

### 2.对于高版本chrome和firefox，可以通过禁用伸缩，即在 head 上的 meta 标签添加 user-scalable = no。如下：

```html
<meta name="viewport" content="width=device-width, user-scalable=no">
```

### 3.chrome32+ 可以将 viewport 的宽度设置成 device-width.

### 4.IE10+，可以使用 pointerEvents。可以让特定的元素或者整个文档中的元素移除点击延迟的问题，同时不会影响 pinch-zooming

```css
a, button, .myelements
{
-ms-touch-action: manipulation;    /* IE10  */
touch-action: manipulation;        /* IE11+ */
}
```

### 5.通过 touchend 事件代替 click 事件

### 6.fastclick.js解决方法

- 终极大 boss。 fastclick。上面的几种方法都是针对某些浏览器，或者某些浏览器的某些版本，或者会影响到我们平常使用方式的解决方案。使用起来不方便且考虑的细节很多，实践难度比较大。fastclick 作为一个终极的解决方案，使用方便，文件大小压缩后只有 3.3k。对于交互相对复杂的移动端web页面或应用是一个相对不错的解决方案。

```html
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title></title>
    <style>
        *
        {
            margin: 0;
        }
        body
        {
        }
        .button
        {
            background-color: #3d3d3d;
            border: 0px;
            height: 80px;
            width: 80%;
            font-size: 50px;
            margin: 10% 0% 0% 10%;
            color: #fff;
        }
        .fu
        {
            min-height: 100%;
            min-width: 100%;
            background-color: Black;
            background: rgba(0,0,0,0.4);
            position: absolute;
            top: 0;
            text-align: center;
            display: none;
        }
        .ts
        {
            margin: 8% auto;
            width: 400px;
            height: 400px;
            top: 59%;
            background-color: #fff;
            text-align: center;
        }
    </style>
    <script src="fastclick.js" type="text/javascript"></script>
    <script src="jquery-1.7.2.js" type="text/javascript"></script>
    //javascript:
    <script type="application/javascript">
        window.addEventListener('load', function () {
            FastClick.attach(document.body);
        }, false);
        function xian() {
            $(".fu").show().hide(350);
        }
    </script>
    //jQuery:
    <script>
        window.addEventListener('load', function () {
$(function() {
        FastClick.attach(document.body);
    });
    </script>
    //CommonJS:
attachFastClick = require('fastclick');
    attachFastClick(document.body);
    AMD:
    var FastClick = require('fastclick');
    FastClick.attach(document.body, options);
</head>
<body>
    <div>
        <div class="but">
            <input class="button" type="button" value="点击我" onclick="xian()" /></div>
        <div class="fu" >
            <div class="ts">
                我是浮层
            </div>
        </div>
    </div>
</body>
</html>
```

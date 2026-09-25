---
# 必填。项目名称。
title: "关于png24格式的图片背景在IE6下显示不透明的解决方法"
# 可选，和文章一样使用。
slug: 关于png24格式的图片背景在IE6下显示不透明的解决方法
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-08-01
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "关于png24格式的图片背景在IE6下显示不透明的解决方法,ie兼容性相关"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Css
tags:
  - Css
  - IE兼容性
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

> 图片透明，锯齿问题是重构人员很头疼的问题:`png8`格式的透明背景图片，会让浏览器在先显示的过程中图片边缘会有一些锯齿情况，`png24`可以解决这些锯齿问题，但是`ie6`不支持`png24`透明

<!-- more -->
## 利用ie6的`hack`问题有两种解决的办法

```html
<div class="pwdTipsBg"></div>
<div class="pwdTips">
    <span class="closeBtn"></span>
    <i class="pwdTipsIcon"></i>
    验证码错误，请填写最新获取的验证码！

</div>
```

### 1.利用ie6的`hack`问题，用两种格式的图片来表示；一种其他浏览器用`png24`格式的图片显示，`ie6`用`png8`格式的显示

```css
.pwdTipsBg{
    height:100%;
    background:#000;
    opacity:0.5;
    position: absolute;
    left:0;
    top:0;
    z-index:1001;
    filter:  alpha(opacity=50);
    width:100%;
    zoom:1;
    }
.pwdTips{
    position:absolute;
    left:40%;
    top:40%;
    z-index:1009;
    width:285px;
    background:#ececec;
    height:55px;
    padding:45px 20px 10px 80px;
    }
.pwdTips i{
    position:absolute;
    left:40px;
    top:40px;
    background-position:-152px -68px; width:26px;       height:26px;
    }

.pwdTips span{
    position:absolute;
    top:-10px;
    right:-15px;
    width:33px;
    height:33px;
    background:url(closebtn.png) no-repeat 0 0;
    _background:url(scsprites.png) no-repeat -119px -63px;
    cursor:pointer;
    display:block;
    }
```

### 2.利用`filter`滤镜解决图片问题

```css
.pwdTips span{
    position:absolute;
    top:-10px;
    right:-15px;
    width:33px;
    height:33px;
    background:url(closebtn.png) no-repeat 0 0;
    _background:none;
    filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src="css/safecenter/closebtn.png");
    cursor:pointer;
    display:block;
    }
```

- 1、书写正常的CSS代码，通过background导入图片，这样所有的浏览器均使用了此PNG图片；

    ```css
    background:url(closebtn.png) no-repeat 0 0;
    ```

- 2、通过滤镜对引入图片，滤镜引入图片的时候是相对于HTML文件，而不是相对于`CSS`文件，语法如下：

    ```css
    filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src="css/safecenter/closebtn.png")
    ```

代码写到这里，我们放到`IE6`下测试后发现`IE6`还是没有透明，因为我们虽然设置了滤镜引入图片，但是`background`也同样加载了此图片，又因为`background`的图层比滤镜设置的高，所以才没有显示出来。所以最终的代码设置为：

```css
pwdTips span{
    position:absolute;
    top:-10px;
    right:-15px;
    width:33px;
    height:33px;
    background:url(closebtn.png) no-repeat 0 0;
    _background:none;
    filter:progid:DXImageTransform.Microsoft.AlphaImageLoader(src="css/safecenter/closebtn.png");
    cursor:pointer;
    display:block;
}
```

#### 优点

- 1、绿色无插件；
- 2、效率高，速度快；
- 3、网速慢的时候，不会出现先灰底再透明的情况，支持远程图片；
- 4、支持Hover等伪类，但是得使用两张图片，网速慢的情况下，会导致第二张图片暂时无法显示，因为还没有完全载入；

#### 缺点

- 1、不支持平铺，虽然filter有sizingMethod="scale", 拉伸缩放模式，但是图片会变形，如果单纯的颜色或简单的渐变色还能横向平铺；
- 2、不支持Img标签；
- 3、不支持CSS Sprite；

> 看到很多人的`logo`有在`ie6`下面显示显示不透明，有一层淡蓝色的底，其它浏览器下都是好，这个是因为用了`png24`格式的图片。

那我们在制作图标的时候应该注意什么呢？（格式，透明，毛边）

## 如何把`png24`透明`logo`转换`png8`格式

- 1. 用`photoshop`软件打开 你要处理的格式为`png24`的`logo`

- 2. `photoshop`菜单:文件—存储为`web`和设备所用格式（或者快捷键 `Alt+Shift+Ctrl+S`）

- 3. 在`png24`那选择`png8`格式，最重要的一点是“杂色”颜色的选项，如果这边没有设置好就会毛刺边出现，这边应该怎么设置呢？

- 4. “杂色”选项的颜色应该选择和`logo`背景颜色最接近的

- 5. 保存一下就可以了。

## png8和png24的区别

- 1.`PNG-8` 与 `PNG-24` 对`IE6`的支持程度
  - `PNG-24`是支持`alpha`通道透明的格式，支持半透明，`IE6`不支持`PNG-24`,但是他完全支持`PNG-8`。
  - 如果是不透明的`PNG-24`,`IE6`也是完美支持,之所以说`IE6`不支持`PNG-24`是因为`PNG-24`的半透明会在`IE6`里显示不正常。
- 2.`PNG-8` 与 `PNG-24` 的透明区别
  - `PNG-8` 和 `gif` 有一些相似之处，模式都是索引颜色，只支持像素级的纯透明，不支持 `alpha` 透明。我们通常说的“`IE6` 不支持 `PNG` 透明”，是指不支持 `PNG-24` 的透明（将透明区域显示为灰色）。但是 `IE6` 支持 `PNG-8` 的透明，就像支持 `gif` 的透明一样。
- 3.`PNG-8` 的高压缩比
  - 切图时，有时选择 `PNG-8` 可以获得更高的压缩比。注意，是 `PNG-8`，不是 `PNG-24`。不过有些情况下还是 `gif` 或 `jpg` 会小一些，需要根据实际情况调试以选择最佳方案。

## `PNG-8` 与 `GIF`

- `PNG-8`跟`GIF`一样支持单色透明。`GIF`有的`PNG-8`都有，`GIF`没有的`PNG-8`还有，比如:同样的文件`PNG-8`格式的却比`GIF`要小

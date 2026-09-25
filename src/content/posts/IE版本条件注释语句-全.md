---
# 必填。项目名称。
title: "IE版本条件注释语句(全)"
# 可选，和文章一样使用。
slug: IE版本条件注释语句(全)
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-20
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "IE版本条件注释语句(全)"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: HTML
tags:
  - HTML
  - IE
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
- IE版本条件注释语句(全)
<!-- more -->
```html
<!--[if lt IE 9]>
<script charset="utf-8" type="text/javascript" src="js/html5.min.js"></script>
<![endif]-->
```

- 1、只有IE才能识别

```html
<!--[if IE]>
<link type="text/css" rel="stylesheet" href="my.css" />
<![endif]-->
```

- 因为只有IE5以上的版本才开始支持IE条件注释，所有“只有IE”才能识别的意思是“只有IE5版本以上”才能识别。

- 2、只有特定版本才能识别

```html
<!--[if IE 8]>
<link type="text/css" rel="stylesheet" href="my.css" />
<![endif]-->
```

- 识别特定的IE版本，高了或者低了都不可以。上例只有IE8才能识别。

- 3、只有不是特定版本的才能识别

```html
<!--[if !IE 7]>
<link type="text/css" rel="stylesheet" href="my.css" />
<![endif]-->
```

- 上例中特定IE7版本不能识别，其他版本都能识别，当然要在IE5以上。

- 4、只有高于特定版本才能识别

```html
<!--[if gt IE 7]>
<link type="text/css" rel="stylesheet" href="my.css" />
<![endif]-->
```

- 上例中只有高于IE7的版本才能识别。IE7无法识别。

- 5、等于或者高于特定版本才能识别

```html
<!--[if gte IE 7]>
<link type="text/css" rel="stylesheet" href="my.css" />
<![endif]-->
```

- 上例中IE7和更高的版本都能识别。

- 6、只有低于特定版本的才能识别

```html
<!--[if lt IE 7]>
<link type="text/css" rel="stylesheet" href="my.css" />
<![endif]-->
```

- 上例中只有低于IE7的版本才能识别，IE7无法识别。

- 7、等于或者低于特定版本的才能识别

```html
<!--[if lte IE 7]>
<link type="text/css" rel="stylesheet" href="my.css" />
<![endif]-->
```

- 上例中IE7和更低的版本可以识别。

- 关键词解释
- 上面那些代码好像很难记的样子，其实只要稍微解释一下关键字就很容易记住了。
- lt ：就是Less than的简写，也就是小于的意思。
- lte ：就是Less than or equal to的简写，也就是小于或等于的意思。
- gt ：就是Greater than的简写，也就是大于的意思。
- gte：就是Greater than or equal to的简写，也就是大于或等于的意思。
- !：就是不等于的意思，跟javascript里的不等于判断符相同。

> 特别提示：

- １、有人会试图使用<!--[if !IE]>来定义非IE浏览器下的状况，但注意：条件注释只有在IE浏览器下才能执行，这个代码在非IE浏览下被当做注释视而不见。
- ２、我们通常用IE条件注释根据浏览器不同载入不同css，从而解决样式兼容性问题的。其实它可以做的更多。它可以保护任何代码块——HTML代码块、JavaScript代码块、服务器端代码……看看下面的代码。

```html
<!--[if IE]>
<script type="text/javascript">
 alert("你使用的是IE浏览器！");
</script>
<![endif]-->
```

```html
<!–[if !IE]><!–><!–<![endif]–><!–除IE外都可识别（IE10版本以上也可以识别）–>
<!–[if IE]><![endif]–><!–IE9以及以下版本可识别–>
<!–[if IE 5]><![endif]–><!–仅IE5可识别–>
<!–[if IE 5.0]><![endif]–><!–仅IE5.0可识别–>
<!–[if IE 5.5]><![endif]–><!–仅IE5.5可识别–>
<!–[if IE 6]><![endif]–><!–仅IE6可识别–>
<!–[if IE 7]><![endif]–><!–仅IE7可识别–>
<!–[if IE 8]><![endif]–><!–仅IE8可识别–>
<!–[if IE 9]><![endif]–><!–仅IE9可识别–>
<!–[if lt IE 5]><![endif]–><!–IE5以下版本可识别–>
<!–[if lt IE 5.0]><![endif]–><!–IE5.0以下版本可识别–>
<!–[if lt IE 5.5]><![endif]–><!–IE5.5以下版本可识别–>
<!–[if lt IE 6]><![endif]–><!–IE6以下版本可识别–>
<!–[if lt IE 7]><![endif]–><!–IE7以下版本可识别–>
<!–[if lt IE 8]><![endif]–><!–IE8以下版本可识别–>
<!–[if lt IE 9]><![endif]–><!–IE9以下版本可识别–>
<!–[if lte IE 5]><![endif]–><!–IE5以及IE5以下版本可识别–>
<!–[if lte IE 5.0]><![endif]–><!–IE5.0以及IE5.0以下版本可识别–>
<!–[if lte IE 5.5]><![endif]–><!–IE5.5以及IE5.5以下版本可识别–>
<!–[if lte IE 6]><![endif]–><!–IE6以及IE6以下版本可识别–>
<!–[if lte IE 7]><![endif]–><!–IE7以及IE7以下版本可识别–>
<!–[if lte IE 8]><![endif]–><!–IE8以及IE8以下版本可识别–>
<!–[if lte IE 9]><![endif]–><!–IE9以及IE9以下版本可识别–>
<!–[if gt IE 5]><![endif]–><!–IE5以上版本可识别–>
<!–[if gt IE 5.0]><![endif]–><!–IE5.0以上版本可识别–>
<!–[if gt IE 5.5]><![endif]–><!–IE5.5以上版本可识别–>
<!–[if gt IE 6]><![endif]–><!–IE6以上版本可识别–>
<!–[if gt IE 7]><![endif]–><!–IE7以上版本可识别–>
<!–[if gt IE 8]><![endif]–><!–IE8以上版本可识别–>
<!–[if gt IE 9]><![endif]–><!–IE9以上版本可识别–>
<!–[if gte IE 5]><![endif]–><!–IE5以及IE5以上版本可识别–>
<!–[if gte IE 5.0]><![endif]–><!–IE5.0以及IE5.0以上版本可识别–>
<!–[if gte IE 5.5]><![endif]–><!–IE5.5以及IE5.5以上版本可识别–>
<!–[if gte IE 6]><![endif]–><!–IE6以及IE6以上版本可识别–>
<!–[if gte IE 7]><![endif]–><!–IE7以及IE7以上版本可识别–>
<!–[if gte IE 8]><![endif]–><!–IE8以及IE8以上版本可识别–>
<!–[if gte IE 9]><![endif]–><!–IE9以及IE9以上版本可识别–>
```

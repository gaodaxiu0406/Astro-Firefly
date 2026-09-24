---
# 必填。项目名称。
title: "HTML基本结构"
# 可选，和文章一样使用。
slug: HTML基本结构
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-30
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "HTML基本结构"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: HTML
tags:
  - HTML
  - CSS
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
## html的基本结构
<!-- more -->
```html
<!DOCTYPE html>
文档声明：必须放在html文件的第一行；如果没有文档声明会触发浏览器的怪异模式
<html>
html元素：告知浏览器，我是一个html文件
    <head>
    head元素：文档的头部，一般放在文档头部的内容不会显示在浏览器的可视区内
    <meta charset="utf-8">规定一个语法
    必须放在head的第一部分
    <title>标题，显示在浏览器的页卡位置，title中的内容也会被seo抓取</title>
    <body>供用户浏览的所有内容，标签、图片、文本、视频···</body>
    </head>
</html>
```
- 一个html文件也叫做一个网页，可以称作是一个文档(document)
- 这个文档从html元素开始，一致向下分支延伸，像一颗大树一样，所以我们将html元素叫做这个文档的**根元素**

`<!DOCTYPE html>`html5的文档声明

- 作用：定义这个文档类型，浏览器先识别这句话，会按照定义的类型去解析这个文档

- html5的文档声明，那么浏览器就会按照html5的规则解析整个页面
`<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
        "http://www.w3.org/TR/html4/loose.dtd">html4版本的文档声明`

- 所有高版本都会向下兼容，所以在以后的工作中，我们直接将文档声明写错html5就可以了
- 文档声明必须写在html文件的第一行
- 文档声明不区分大小写
- 如果html文件没有文档声明，会触发浏览器的怪异模式
- 文档声明不是一个html标签

### 1.html元素
此元素告知浏览器其自身是一个html元素
是由开始和结束标签组成的，html文件里面所有的内容都会放在这个这个元素内
### 2.head元素
    - 整个文档的头部，head元素自带隐藏功能，display:none;里面的内容不会隐藏，只不过一般放置在head元素中的其他元素和内容也是自带隐藏功能的，例如link、script、meta···
    - `<script></script>与head标签一样具有隐藏功能，写在其内的内容在网页不显示`
### 3.`<meta charset="UTF-8">`
### 4.`<meta>`规定了html文档的元信息
- charset="UTF-8" 文档的编码
    - UTF-8 国际通用编码
    - gbk 国标
    - gb2312 国标
- name="keyword" content="关键词"
    - name="keyword" content="HTML5J5..."
    - SEO优化有关
    - SEO搜索引擎
`<meta name="keyword" content="关键词">`
`<meta name="description" content="勿忘初心,方得始终">`

### 5.title元素
- html文档名称 一个页面只有一个title元素
放文字 显示在浏览器的页卡（页头）位置
### 6.link标签
- `<link href="favicon.ico" type="image/x-icon" rel="shortcut icon">`
    - 图标让设计师生成
    - 一般整个图片放在整个项目的根目录下
    - 显示在浏览器页卡位置，title内容之前
- `<link rel="stylesheet" herf="url" type="texe/css">`
    - 引入一个外部的css文件
    - rel不能缺少 stylesheet样式表
    - type可以省略 但是建议写全

### 7.body元素
- 定义整个文档的主体部分，所有展示给用户的内容都要放在这个元素中
- body中有常用的html元素（div、ul），文本内容、音频、视频、图片、表单
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UIF-8">
        <title></title>
    </head>
</html>
```






---
# 必填。项目名称。
title: "CSS中常用的HTML元素及标签"
# 可选，和文章一样使用。
slug: CSS中常用的HTML元素及标签
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-30
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "CSS中常用的HTML元素及标签"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: CSS
tags:
  - CSS
  - HTML
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
### 常用的HTML标签总结
- 1. div 无意义标签，用来区分网页大模块，例如网页头部、主题内容、尾部
<!-- more -->
`<div>无意义元素，用它来区分网页大模块</div>`
```html
banner
<div>区分模块
    <a href="http://www.baidu.com">
        <img src="pic.jpg" alt="备注/描述">
    </a>
    <a href="">
        <img src="" alt="图片加载出问题了" width="100px" height="100px">
    </a>
</div>
```
- 2. span 无意义标签,用来描述行内某个小模块
- 3. p `<p>段落</p>`
- 4. ul li 无序列表
- 5. ol li 有序列表
- 6. b 加粗
- 7. strong 加粗,浏览器解析的时候,有强调作用
- 8. body 身体,网页主体部分 （内容在浏览器可视区显示）
- 9. a 超链接,描点
```html
点击元素可以进行跳转的
<a href="链接路径" target="_blank">珠峰培训</a>
<a href="pic.jpg" target="_blank">珠峰培训</a>
```
- 10. img 插入图片
```html
<img src="图片路径" alt="备注/描述">
<img src="pic.jpg" alt="备注/描述">
```
- 11. i 作用：_斜体_
- 12. em 强调 作用：*斜体
- 13. h1-h6 标题
- 14. dl-dt-dd定义列表 常用在新闻标题和摘要
        - dt 定义标题
        - dd 定义描述
        - 一个dt可以多个dd进行描述

## 标签
- 标签（由尖括号和关键字组成的超文本）
- 关键字（就是普通文本），在编辑html这门语言的时候，相关组织将这些文本归纳到了一定的规则中，是他有了特殊的含义和作用
- 标签的分类：开始标签、结束标签、空标签
```html
<开始标签><空标签 />
<div></div>
<b></b>
<strong></strong>
<ul><li></li></ul>
<ol><li></li></ol>
<p></p>···
</结束标签>
```
- 标签属性：用来描述标签功能的，一般写在开始标签中，跟在标签名的后面，用空格隔开，一个标签可以有很多标签属性，每一个属性都用空格隔开
```html
<开始标签 属性名="属性值" 属性名1="属性值"><结束标签>
<img src="url" alt="备注" />
```

### html标签
- 1. html标签HTML 元素指的是从开始标签（start tag）到结束标签（end tag）的所有代码。

- 标签不会出现在页面中，只有标签中的内容才会显示在页面上 ：也就是`<html>此处为内容</html>`

- 标签不区分大小写，但是推荐使用小写 ：(X)HTML 版本中强制使用小写，这样更加严谨

- 标签分为闭合标签和空标签 ：闭合标签是指由开始标签和结束标签组成的一对标签，这种标签允许嵌套和承载内容，例如：`<html></html>、<p></p>`；空标签是没有内容的标签，在开始标签中自动闭合，例如：`<img />、<br />、<hr />等`

## 元素
- 由标签（开始和结束标签中有内容）和内容组成，元素中内容可以为空，一个空标签也叫做一个元素
  ```html
  <div>content</div>-->div元素
  <img src="url" alt="备注" />-->img元素
  ```

  - 标签属性经过html的进化，舍弃了有关样式的标签属性，保留功能的标签属性
  - 例如舍弃width bgcolor align，这些样式描述都放在css里面
  - 保留alt title src href···

## iframe标签
在引入其他文件的时候，必须写宽度和高度
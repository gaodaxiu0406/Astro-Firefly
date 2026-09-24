---
# 必填。项目名称。
title: "HTML标签分类"
# 可选，和文章一样使用。
slug: HTML标签分类
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-30
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "HTML标签分类"
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
### html标签分类
- html标签又叫做html元素，它分为块级元素和内联元素（也可以叫做行内元素），都是html规范中的概念。
<!-- more -->
    - 块级元素
    - 块级元素是指本身属性为display:block;的元素。因为它自身的特点，我们通常使用块级元素来进行大布局（大结构）的搭建
    - 块级元素的特点：
    - 1. 独占一行，每一个块级元素都会从新的一行重新开始，从上到下排布
    - 2. 可以直接控制宽度、高度以及盒子模型的相关css属性
    - 3. 在不设置宽度的情况下，块级元素的宽度是它父级元素内容的宽度
    - 4. 在不设置高度的情况下，块级元素的高度是它本身内容的高度
        - 常用的块级元素:
        - div 常用块级容器，也是css layout的主要标签
        - h1 大标题
        - h2 副标题
        - h3 三级标题
        - h4 四级标题
        - h5 五级标题
        - h6 六级标题
```html
标题：
<h1>一级标题</h1>
<h2>二级标题</h2>
h${$级标题}*6+tab生成：
<h1>1级标题</h1>
<h2>2级标题</h2>
<h3>3级标题</h3>
<h4>4级标题</h4>
<h5>5级标题</h5>
<h6>6级标题</h6>
```
- hr 水平分隔线
- menu 菜单列表
- ol 有序列表 li列表项
```html
有序列表
<ol>
    <li>盗天仙图</li>
    <li>名侦探</li>
    <li>鬼吹灯</li>
    <li>盗墓笔记</li>
    <li>名侦探</li>
    <li>鬼吹灯</li>
</ol>
```

- ul 无序列表 li列表项

```html
无序列表
<ul>
    <li><span style="color:red">√<b>有保证</b></span>:先学习考试后入学</li>
    <li><span style="color:red">√<b>有实力</b></span>:专注JS培训七年铸就传奇就业,平均工资超12K</li>
    <li><span style="color:red">√<b>有深度</b></span>:结合的大学算法和数据结构的基础课</li>
    <li><span style="color:red">√<b>重原生</b></span>:狠练原生代码,原生JS+Node才是王道</li>
    <li><span style="color:red">√<b>重应用</b></span>:PC+移动端+H5+CSS3+node的前后台全栈项目</li>
    <li><span style="color:red">√<b>重未来</b></span>:app开发,微信开发,angular,es6,前沿技术</li>
</ul>
```

- dl 定义列表 dt 定义术语 dd定义描述
- table 表格
- p 段落
```html
<div class="poem">
<h4>早发白帝城</h4>
<h5>作者：李白</h5>

<p>朝辞白帝彩云间，<br>
    千里江陵一日还。<br>
    两岸猿声啼不尽，<br>
    轻舟已过万重山。<br>
    <img src="timg.jpg" alt="李白">
</p>
</div>
```

```html
<div>
    <h4 align="center">早发白帝城</h4>
    <h5 align="center">作者：李白</h5>
    <p align="center">朝辞白帝彩云间，</p>
    <p align="center">千里江陵一日还。</p>
    <p align="center">两岸猿声啼不尽，</p>
    <p align="center">轻舟已过万重山。</p>
    <img src="timg.jpg" alt="李白">
</div>
```

- form 交互表单

- 内联元素
- 内联元素是指本身属性为display:inline;的元素。因为它自身的特点，我们通常使用块级元素来进行文字、小图标（小结构）的搭建。

- 内联元素的特点：
- 1. 和其他内联元素从左到右在一行显示
- 2.不能直接控制宽度、高度以及盒子模型的相关css属性，但是直接设置内外边距的左右值是可以的
- 3.内联元素的宽高是由本身内容的大小决定（文字、图片等）
- 4.内联元素只能容纳文本或者其他内联元素（此处请注意，不要在内联元素中嵌套块级元素）
- 常用的内联元素:
- span 常用内联容器，定义文本内区块
- a 锚点
- 文本设置类:
    - b 加粗
    - strong 加粗强调
    - i 斜体
    - em 斜体强调
    - s 中划线（不推荐使用）
    - strike 中划线
    - del 文档中已被删除的文本
    - big 大字体文本、small小字体文本）
    - small 小字体文本
    - br 强制换行
    - u 下划线
    - textarea 多行文本输入框
    - input 输入框
    - select 下拉列表
    - label（input 元素定义标注/标记）、img
    - sub 下标
    - sup 上标

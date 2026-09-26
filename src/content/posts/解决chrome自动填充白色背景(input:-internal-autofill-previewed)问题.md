---
# 必填。项目名称。
title: "解决chrome自动填充白色背景(input:-internal-autofill-previewed)问题"
# 可选，和文章一样使用。
slug: 解决chrome自动填充白色背景(input:-internal-autofill-previewed)问题
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2019-09-09
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "解决chrome自动填充白色背景(input:-internal-autofill-previewed)问题"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: CSS
tags:
  - CSS
  - input
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

#### 解决chrome自动填充白色背景(input:-internal-autofill-previewed)问题

> 使用background-clip属性，使它的值为 content-box(将背景裁剪到内容框)，再设input的高度为0，最后使用padding将input框撑开即可：

```css
input:-webkit-autofill {
  height: 0;
  border: 0;
  background-clip: content-box;
  padding: 12px 5px 12px 44px;
}
```

- 然而，有的项目在使用鼠标点选账号密码时依旧会出现灰色背景，最后的解决办法也是误打误撞，将background-clip的权重提到最高content-box!important就行，不会再出现灰色背景。

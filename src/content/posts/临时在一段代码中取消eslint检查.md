---
# 必填。项目名称。
title: "临时在一段代码中取消eslint检查"
# 可选，和文章一样使用。
slug: 临时在一段代码中取消eslint检查
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2019-09-01
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "临时在一段代码中取消eslint检查"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Eslint
tags:
  - eslint
  - Eslint
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

### 临时在一段代码中取消eslint检查

可以如下设置

- 临时在一段代码中取消个别规则的检查（如no-alert, no-console）：`/* eslint-disable no-alert, no-console */`

- 在整个文件中取消eslint检查：`/* eslint-disable */`

- 在整个文件中禁用某一项eslint规则的检查：`/* eslint-disable no-alert */`

- 针对某一行禁用eslint检查：

  - 当前行禁用eslint检查 `alert(‘foo’); // eslint-disable-line`

  - 下一行禁用eslint检查

    ```js
    // eslint-disable-next-line
    alert(‘foo’);
    ```

- 针对某一行的某一具体规则禁用eslint检查：

  - 当前行禁用eslint检查 `alert(‘foo’); // eslint-disable-line no-alert`

  - 下一行禁用eslint检查

    ```js
    // eslint-disable-next-line no-alert 
    alert(‘foo’);
    ```

- 针对某一行禁用多项具体规则的检查：

  - 当前行禁用eslint检查 `alert(‘foo’); // eslint-disable-line no-alert, quotes, semi`

  - 下一行禁用eslint检查

    ```js
    // eslint-disable-next-line no-alert, quotes, semi 
    alert(‘foo’);
    ```

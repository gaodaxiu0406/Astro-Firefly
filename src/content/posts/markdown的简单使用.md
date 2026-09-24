---
# 必填。项目名称。
title: "markdown的简单使用"
# 可选，和文章一样使用。
slug: markdown的简单使用
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-30
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "markdown的简单使用"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: markdown
tags:
  - markdown
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
- #--> 一级标题 相当于html中的h1标签

- [TOC]-->目录
<!-- more -->
- ##--> 二级标题 相当于html中的h2标签

- ###--> 三级标题 相当于html中的h3标签

- ####--> 四级标题 相当于html中的h4标签

- #####--> 五级标题 相当于html中的h5标签

- ######--> 六级标题 相当于html中的h6标签

- 在每个段落或标题结束后 增加一个回车（一行空白）
- 普通段落相当于html中的p标签

### 列表

- `-`+`空格`（-列表-）
- `-`+`空格`+`tab`（二级列表）
- `-`+`空格`+`tab`+`tab`（三级列表）
- 如何缩进 --> 点击`tab`键
- 编辑新的内容（英文状态下，按住`shift`+`—`）

### `>` (大于号加空格)--> 摘要或标注

### 编辑表格:左边有冒号代表左对齐,右边有冒号代表右对齐,两边都有冒号代表居中

- 快捷键：`ctrl+alt+T`
- |标题|标题|标题|
- |:----|----:|:----:|
- |左对齐|右对齐|居中|
- 例如:

|标题|标题|标题|
|:----|----:|:----:|
|左对齐左对齐左对齐|右对齐右对齐右对齐|居中居中居中居中|
|内容|内容|内容|

### 编辑代码块`<div>div</div>`

```css
<div>div</div>
<div>div</div>
<div>div</div>
```

### 编辑行内代码:独立的行间代码

- `html`中的`p`标签：`<p>`

### 插入图片

- 可以直接复制粘贴
- 快捷键：`ctrl+G`

### 插入链接

- `ctrl+L`

### 保存笔记的方法

- 点击【账号】选择【导出】 -->  可以导出`md`格式，`pdf`格式，`html`格式
  - `md`格式：再次打开时，可以使用文本文档打开，将内容复制一份粘到`markdown`软件中
  - `pdf`格式：直接观看，但不能修改
  - `html`格式：可以浏览器中直接观看，可以在代码编辑器中修改

## 快捷键

- 文档管理 --> Ctrl+O
- 帮助 --> Ctrl+/
- 最大化编辑器 --> Ctrl+Enter
- 预览文档 --> Ctrl+Alt+Enter
- 同步文档 --> Ctrl+S
- 创建文档 --> Ctrl+Alt+N
- 系统菜单 --> Ctrl+M
- 斜体 --> Ctrl+I
- 粗体 --> Ctrl+B

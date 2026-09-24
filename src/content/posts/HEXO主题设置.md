---
# 必填。项目名称。
title: "HEXO主题设置(huno主题)"
# 可选，和文章一样使用。
slug: HEXO主题设置(huno主题)
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-07-31
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "HEXO主题设置(huno主题)"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: HEXO
tags:
  - HEXO
  - 博客
  - huno
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
- 目前使用的主题是：next
- 当前文章所述主题为：huno
- 在博客的根目录下（即上一篇文章基于GitHub创建自己的博客`https://gaodaxiu0406.github.io/2017/04/25/%E5%9F%BA%E4%BA%8EGitHub%E5%88%9B%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A%E5%AE%A2/`中提到的 HEXO 文件夹下） 克隆主题
<!-- more -->
## 克隆主题
```js
git clone git://github.com/someus/huno.git themes/huno
```
- 提示:huno的github地址:https://github.com/gaodaxiu0406/huno
### 执行：
```js
vim _config.yml
```
- 执行此命令后可以对此文档进行编辑 输入o进入编辑状态
### 将 theme 对应的值进行修改
```js
theme: huno
```
- 修改完成 按esc键退出编辑状态 再输入:wq退出编辑窗口模式
## 自动部署
```js
npm install hexo-deployer-git --save
```
## 发布
```js
hexo clean && hexo g && hexo d
```
- 稍等片刻看一下自己的博客主页，你想要的效果就出现了。也可以在github或百度中搜索更多主题，挑选自己喜欢的主题进行修改，只要你快乐就好

## 主题配置
- 现在主题是更改过来了，但还有许多细节需要处理，比如说你需要修改头像等等。
- 每个人的设置风格不同,但基本的设置在你下载的主题中的README文件中都有介绍,你可以按照文件中的介绍配置属于自己的博客。动气手来，让你的博客亮起来

##### 返回上篇:基于GitHub创建自己的博客`https://gaodaxiu0406.github.io/2017/04/25/%E5%9F%BA%E4%BA%8EGitHub%E5%88%9B%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E5%8D%9A%E5%AE%A2/`
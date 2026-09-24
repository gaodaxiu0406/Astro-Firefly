---
# 必填。项目名称。
title: "HEXO常用命令"
# 可选，和文章一样使用。
slug: HEXO常用命令
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2018-07-15
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "HEXO常用命令"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: HEXO
tags:
  - HEXO
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

## hexo安装

```js
npm install hexo -g //安装
npm update hexo -g //升级
hexo init //初始化
```
<!-- more -->

## hexo命令

```js
hexo n "我的博客" //新建文章-简写
hexo new "我的博客" //新建文章
hexo new page "title" //新建页面
hexo new post "title" //写作
hexo new photo "My Gallery" //模版
hexo p //草稿-简写
hexo publish [layout] <title> //草稿
hexo g //生成静态页面至public目录 使用 Hexo 生成静态文件快速而且简单 -简写
hexo generate //生成静态页面至public目录 使用 Hexo 生成静态文件快速而且简单
hexo generate --watch //监视文件变动
hexo s //启动服务预览/开启预览访问端口（默认端口4000，'ctrl + c'关闭server）-简写
hexo server //启动服务预览/开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo d //开始部署，将.deploy目录部署到GitHub-简写
hexo deploy //将.deploy目录部署到GitHub
hexo server //Hexo 会监视文件变动并自动更新，您无须重启服务器。
hexo server -s //静态模式
hexo server -g //完成后部署
hexo server -p 5000 //更改端口为5000
hexo server -i 192.168.1.1 //自定义 IP
hexo clean //清除缓存 网页正常情况下可以忽略此条命令
hexo generate --deploy //完成后部署
hexo deploy --generate //完成后部署
hexo d -g //完成后部署-简写
```

<!-- 参考地址:`https://segmentfault.com/a/1190000002632530` -->
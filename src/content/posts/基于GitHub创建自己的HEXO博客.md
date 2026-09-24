---
# 必填。项目名称。
title: "基于GitHub创建自己HEXO的博客"
# 可选，和文章一样使用。
slug: 基于GitHub创建自己HEXO的博客
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2018-07-04
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "基于GitHub创建自己HEXO的博客"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: HEXO
tags:
  - HEXO
  - 博客
  - GitHub
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
## 搭建环境准备
- Node.js 的安装和准备
- Git的安装和准备
- gitHub账户的配置
<!-- more -->
### Node.js 的安装和准备

- 1.下载node.js安装文件：https://nodejs.org/en/
- 2.cmd，打开命令行界面,查看安装版本

```js
node -v
npm -v
```
### 配置Git环境
- 下载Git安装文件：https://git-scm.com/downloads
- 打开命令行输入,检查安装是否成功

```js
git --version
```
### github账户的注册和配置
- Github注册：https://github.com/
- 创建代码库：
- 在Repository name下填写yourname.github.io，Description (optional)下填写一些简单的描述（不写也没有关系

```js
注意：
比如我的github名称是gaodaxiu0406 ,
这里你就填 gaodaxiu0406.github.io
```
- 代码库设置:Setting
   + 接下来开启gh-pages功能，点击界面右侧的Settings，你将会打开这个库的setting页面，向下拖动，直到看见GitHub Pages
   + 点击Automatic page generator，Github将会自动替你创建出一个gh-pages的页面

## 安装Hexo
- 首先在E盘(选择你的HEXO存放的文件夹,最好不要安装到C盘)目录下创建Hexo文件夹，并在命令行的窗口进入到该目录

```js
E:    进入E盘
cd Hexo 进入Hexo文件夹

```
- 安装HEXO

```js
npm install hexo-cli -g
```
- 可能你会看到一个WARN，但是不用担心，这不会影响你的正常使用。

### 检查安装是否成功
```js
hexo -v
```

## hexo的相关配置

### 初始化Hexo

```js
hexo init
npm install
```

### 首次体验Hexo

```js
hexo g   #生成
hexo s   #启动服务
```
在浏览器中打开http://localhost:4000/ 即可预览你的HEXO页面

## 怎样将Hexo与github page 联系起来

### 大概分为以下几步:
- 配置git个人信息
- 配置Deployment

### 配置Git个人信息
- 1.设置Git的user name和email：(如果是第一次的话)

  ```js
  git config --global user.name "gaodaxiu0406"
  git config --global user.email "1260833716@qq.com"
  ```
- 2.检查是否已经有SSH Key(密钥)。
  ```js
  cd ~/.ssh
  ls
  ```
- 3.生成密钥(如果没有密钥的话)
  ```js
  ssh-keygen -t rsa -C "1260833716@qq.com"
  ```

  ```js
  连续3个回车。如果不需要密码的话。
  最后得到了两个文件：id_rsa和id_rsa.pub。
  默认的存储路径是：C:\Users\Administrator\.ssh
  ```
- 4.添加密钥到ssh-agent

  ```js
  eval "$(ssh-agent -s)"
  ```
  添加生成的 SSH key 到 ssh-agent。

  ```js
  ssh-add ~/.ssh/id_rsa
  ```
- 5.登陆Github, 添加 ssh
    - 把id_rsa.pub文件里的内容复制到SSH keys

- 6.测试：

  ```js
  ssh -T git@github.com
  ```
  - 你将会看到：如果看到Hi后面是你的用户名，就说明成功了。

  ```js
  如果提示Are you sure you want to continue connecting (yes/no)?，输入yes
  ```
### 配置Deployment
- 配置_config.yml中有关deploy的部分：

  ```js
  deploy:
  type: git
  repository: git@github.com:gaodaxiu0406/gaodaxiu0406.github.io.git
  branch: master

  ```
## 写博客、发布文章
- 1.定位到我们的hexo根目录，执行命令：

  ```js
  hexo new 'my-first-blog'
  ```
- hexo会帮我们在HEXO文件夹-->source文件夹-->_posts文件夹下生成相关.md文件,用马克飞象打开写文章就可以
- 文章编辑好之后，运行生成、部署命令：

  ```js
  hexo g   // 生成
  hexo d   // 部署
  ```
  或者(合并写法)

  ```js
  hexo d -g #在部署前先生成
  ```

### 踩坑提醒
```js
deloyer not found:git
```
 - 这样的错误是需要装插件

 ```js
 npm install hexo-deployer-git --save
 ```

##### 下篇:HEXO主题设置`https://gaodaxiu0406.github.io/2017/07/31/HEXO%E4%B8%BB%E9%A2%98%E8%AE%BE%E7%BD%AE/`
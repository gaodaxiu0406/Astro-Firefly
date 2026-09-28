---
# 必填。项目名称。
title: "使用Astro搭建个人博客2"
# 可选，和文章一样使用。
slug: 使用Astro搭建个人博客遇到的问题
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2026-09-25
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: true
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "使用Astro搭建个人博客遇到的问题"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: 博客指南
tags:
  - Astro
  - 博客
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

## Mac 显示隐藏文件的快捷键

Mac 显示隐藏文件的快捷键是 ‌Command + Shift + .（点号）‌。在访达窗口中按下此组合，隐藏文件会显示，再按一次恢复隐藏。

## 怎么用 pnpm 自带功能切换

- ‌全局切换‌：使用命令 `pnpm env use --global <version>`，如 `pnpm env use --global 18`。
- ‌查看版本‌：执行 `pnpm env ls` 可列出已安装的 `Node` 版本。
- ‌清理旧版‌：使用 `pnpm env remove <version>` 卸载不再需要的 `Node` 版本。
- ‌修复 `pnpm` 失效‌：切换 `Node` 版本后，`pnpm` 可能报“不是内部或外部命令”，需在新版本下重新全局安装 `pnpm`（`npm install -g pnpm`。
- 缓存隔离‌：可通过配置 `PNPM_HOME` 环境变量，让不同 `Node` 版本使用独立的 `pnpm` 全局工具目录，避免冲突。

> 怎么让项目自动切换版本

- ‌锁定版本‌：在项目根目录创建 `.npmrc` 文件，添加 `use-node-version=18.17.0`。
- ‌自动生效‌：配置后，在该目录下运行 `pnpm` 令时会自动切换到指定 `Node` 版本，无需手动干预。
- ‌兼容检查‌：建议配合 `package.json` 中的 `engines` 字段，强制检查 `Node` 版本是否符合项目要求。‌‌‌

## git常用命令

```js
```
<!-- 

### 5.1 创建与部署项目

这里 `Vercel` 导入项目就直接强制执行一次部署，而且部署分支是默认的，在这时还不能改，这个设定有点难绷……

而我们前文指定了`master`分支是用来跟踪主题更新的，`dev`才是我们博客源码所在的分支，所以首先我们要把`Vercel`项目的部署分支设置为`dev`。

1. 打开项目设置>Environments>Production，将分支修改过来后点击保存。

图片？？？

这样我们的`Vercel`项目跟踪的就是`dev`分支，每次推送到该分支的提交， `Vercel` 都会自动帮我们创建一个生产部署（也就是自动更新我们线上的博客）。

2. 然后前往`Vercel`官网注册账号，创建一个新项目：

图片？？？

授权你的`Github`账户，导入你的`Astro`博客仓库：

图片？？？

`Vercel`自动识别出了`Astro`项目，帮我们做好了部署配置，无需任何修改，直接点击`Deploy`：

图片？？？

我们后续只需要再往`dev`分支推送一次新的提交，就可以触发 `Vercel` 项目的自动部署。

自动部署未触发时，可检查提交作者的邮箱是否与你的 `Vercel` 账户邮箱一致（若通过 `GitHub` 登录，则需匹配关联的 `GitHub` 账号邮箱）。 -->

```js
// 卸载node
sudo rm -rf /usr/local/bin/node /usr/local/bin/npm /usr/local/bin/npx
sudo rm -rf /usr/local/lib/node_modules /usr/local/include/node
sudo rm -rf /usr/local/share/doc/node /usr/local/share/man/man1/node.1 /usr/local/lib/dtrace/node.d
```

### 5.1 检查

首先需要检查你的邮箱是否是你的`GitHub`邮箱，如果邮箱不一致，需要修改为正确的邮箱

```js
// 查询邮箱
git config --global user.email

// 修改为正确的邮箱
git config --global user.email "xxx@xxx.com"
```

这里我使用`Vercel`，主要是`Vercel`原生支持`Astro`项目，不需要复杂的配置，只需要导入你的`Astro`项目仓库即可。

<!-- 更多git命令请前往[git常用命令统计]？？？ -->

<!-- ### 3.5 同步原主题仓库更新

这是原主题作者发布更新（如修复 Bug、新增功能）后，你需要把这些更新同步到自己仓库的操作，核心是 “先更新干净的 master 分支，再合并到开发分支”。

GitHub 网页端同步你的 Fork 仓库（更新 master 分支）：

- 当原仓库有更新后，你的Fork 仓库会有如下图所示提示
- 点击 `Sync fork` > `Update branch` 同步更新

截图blog-？？？

先让 master 分支同步原仓库最新代码，再将更新合并到你的 dev 分支，冲突只在「开发分支」解决，不影响主分支。

步骤 1：更新本地 master 分支

```js
// 1. 切到master分支
git checkout master 

// 2. 拉取Fork仓库更新
git pull
```

步骤 2：合并到你的开发分支

```js
// 1. 切回开发分支 
git checkout dev 

// 2. 合并更新后的 master 分支到开发分支 
git merge master 

// 3. 若有冲突，本地解决后提交
git add . # 标记冲突文件已解决
git commit -m "merge: 同步主题更新，解决xxx文件冲突"
git push
```

图片？？？

### 3.6 私有化仓库

对于不想公开自己的博客仓库、希望将其设置为私有化的博主来说，由于 GitHub 上 fork 的仓库不支持直接设为私有，我们可按以下步骤操作：首先点击「Leave fork network」，脱离原 fork 网络；随后刷新页面，再点击「Change visibility」，将仓库可见性修改为私有。

图片？？？

图片？？？

脱离 fork 网络并将仓库设为私有后，无法再通过 GitHub 网页端直接同步原仓库的更新。

替代方案：你可以在本地仓库中，手动添加原仓库作为 “上游仓库”，通过 Git 命令行拉取原仓库的更新，修改完成后再推送到自己的私有仓库，就能实现间接同步（全程需在本地操作，无法通过网页端完成）

初始设置（只需做一次）：

```js
// 切换到master分支
git checkout master

// 添加上游仓库
git remote add upstream https://github.com/原始作者/原始仓库名.git

// 检查
git remote -v
```

图片？？？

同步更新（以后每次都这样操作）：

```js
// 切换到master分支
git checkout master

// 从上游仓库主分支拉取最新代码
git pull upstream master

// 推送到你的私有仓库
git push
```

最后再按照前文的教程，将更新合并到你的开发分支即可。 -->

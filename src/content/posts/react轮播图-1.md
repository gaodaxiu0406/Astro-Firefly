---
# 必填。项目名称。
title: "React轮播图（上）"
# 可选，和文章一样使用。
slug: React轮播图项目配置及原理概要
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-07-31
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "React轮播图项目配置及原理概要"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: React
tags:
  - React
  - 轮播图
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

## 项目配置及原理概要

## 1.初始化项目

```js
npm init -y
```

- 生成`package.json`文件

<!-- more -->

## 2.安装依赖包 开发依赖

```js
npm install webpack webpack-dev-server babel-core babel-loader babel-preset-react babel-preset-es2015 babel-preset-stage-0 style-loader css-loader less-loader less file-loader url-loader html-webpack-plugin -D
```

- `webpack` 打包
- `webpack-dev-server` 用来启动一个`HTTP`服务器预览我们的项目
- `babel-core`、`babel-loader` 进行转译 把`es6`和`react`代码转译成`es5`
- `babel-preset-react` 用来转译`react`
- `babel-preset-es2015` 用来转译`es6`
- `babel-preset-stage-0` 用来转译`es7`
- `style-loader`、`css-loader` 用来处理`css`
- `less-loader`、`less` 编译`less`
- `file-loader`、`url-loader` 用来处理资源文件
- `html-webpack-plugin` 用来自动产出`html`文件
- `open-browser-webpack-plugin` 自动打开浏览器

## 3.安装生产依赖

```js
npm install react react-dom -S
```

## 4.配置文件的出入口路径

- 新建一个`webpack.config.js`文件，在文件中配置入口文件和出口路径

```js
let path=require('path');
module.exports={
    entry:'./src/index.js',//入口文件
    output:{//出口配置
        path:path.resolve('build'),//出口文件路径
        filename:'bundle.js'//出口文件名称
    }
};
```

## 5.启动安装的模块文件夹`node_modules`-->`.bin`-->`webpack.cmd`和`webpack-dev-server.cmd`文件

- 在`package.json`文件中的`scripts`标签进行匹配

```js
"scripts": {
    "build": "webpack",
    "dev":"webpack-dev-server"
  },
```

### 5-1.启动`webpack`和`webpack-dev`

- 在`cmd`中执行命令

```js
npm run build
```

- 1) 在cmd窗口中显示

```js
    Asset     Size  Chunks             Chunk Names
bundle.js  2.52 kB       0  [emitted]  main
   [0] ./src/index.js 43 bytes {0} [built]
```

表示生成`bundle.js`一个文件

- 2) 在当前项目文件夹下会自动生成一个`build`文件夹，同时在`build`文件夹下会自动生成`bundle.js`文件，我们的入口文件(`src`文件夹下的`index.js`)会自动打包到出口文件`bundle.js`中

## 6.自动产出`html`文件

### 6-1.现在我们需要在`build`文件夹中新建一个`index.html`文件，然后引入`bundle.js`进行预览;但是现在我们希望这个文件不要手动创建了，希望他可以自动生成，要做到这一点，我们需要引入插件`html-webpack-plugin`(此插件在最初已经安装过,如果没有安装需安装后才可使用)

- 1) 在`webpack.config.js`中引入`html-webpack-plugin`

```js
let HtmlWebPackPlugin=require('html-webpack-plugin');
```

- 2) 同时给插件再添加个配置项`plugins,plugins`是个数组

```js
plugins:[
    new HtmlWebPackPlugin({
        template:'./src/index.html'
    })
]
```

- 3) `template` 模板 配置到时候会按照哪个模板来自动产出html文件 并且把它自动放到配置目录下-->一般会在`src`文件夹下新建一个模板叫`index.html`。
- 4) 执行`npm run build`

- 4-1) 原理:此时如果再执行`npm run build`的话，就会执行上面配置的`plugins`插件,插件会读取`src`文件夹下的`index.html`模板文件，把他自动插入到打包后的`bundle.js`，并且把`bundle.js`保存到`build`目录下(每次执行`npm run build`命令，都会重新生成`bundle.js`和`index.html`两个文件)

- 4-2) 在`cmd`命令行执行`npm run build`,命令行显示:

```js
     Asset       Size  Chunks             Chunk Names
 bundle.js    2.52 kB       0  [emitted]  main
index.html  188 bytes          [emitted]
   [0] ./src/index.js 43 bytes {0} [built]
```

  表示生成`bundle.js`和`index.html`两个文件,与之前执行`npm run build`相比多了一个`html`文件。

- 4-3) 打开我们的项目文件夹下的`build`文件会发现，已经自动生成了一个出口`index.html`出口文件,打开这个`index.html`出口文件会发现,`index.html`中已经自动引入了`bundle.js`文件

> 关于react轮播图的源码,无缝版已上传至[github,https://github.com/gaodaxiu0406/React-Slider](github,https://github.com/gaodaxiu0406/React-Slider)

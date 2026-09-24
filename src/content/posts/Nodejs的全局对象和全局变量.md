---
# 必填。项目名称。
title: "Nodejs的全局对象和全局变量"
# 可选，和文章一样使用。
slug: Nodejs的全局对象和全局变量
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-27
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "Nodejs的全局对象和全局变量"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/webstore打开设置窗口.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Node
tags:
  - node
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

#### 全局对象

- 所有模块都可以调用
- 1. `global`：表示Node所在的全局环境，类似于浏览器中的`window`对象。
  - 你可以通过`console.log(global);`来输出一下`global`;

<!-- more -->
- 1-1. `global`全局对象里常用的变量
  - 1)   `__dirname` 存储的是在`nodejs`中执行`javascript`所在的绝对目录

    ```js
    console.log(__dirname);
    //C:\Users\Gao\Documents\webstore学习文件\node
    ```

  - 2)  `__filename`  文件名

    ```js
    console.log(__filename);
    //C:\Users\Gao\Documents\webstore学习文件\node\global.js
    ```

- 2. `process` 程序所执行的一些相关的内容信息的封装对象
- 指向`Node`内置的`process`模块，允许开发者与当前进程互动。
  - 例如你在DOS或终端窗口直接输入`node`，就会进入`NODE`的命令行方式（`REPL`环境）。如果要退出的话，可以输入 `process.exit()`;
  - 2-1. 和输出相关的 `process.stdout`/`process.stderr`
    - 1) `process.stdout` -->  `standard output` --> 标准的信息输出
    - 2) `process.stderr` -->  `standard error`  --> 标准的错误输出

      - `console.info`和`console.error`这些相关的输出功能就是调用的`process.stdout`和`process.stderr`来完成的

        ```js
        process.stdout.write("this is stdout");
        process.stderr.write("this is stderr");//红色的
        ```

  - 2-2. `process`如何去监听一些事件
    - 1) `process.stdin.on()`  监听用户输入的键盘信息
    - 2) `process.on()`监听操作系统对`node`发出的一些信号

  - 2-3. 如何读取输入用户的键盘输入
    - 1) `process.stdin`
      - 在使用`process.stdin`之前  要先对他进行一下编码设置

      ```js
      process.stdin.setEncoding("utf-8");
      //这里的编码设置和平常编写网页时候的文本编码不一样
      //在这里如果想读取纯文本信息  只要把他的编码设置成utf-8就可以了   不需要去考虑类似jbk或者jb2312来区分是不是中文
      //on方法来监听用户相关的输入事件
      // process.stdin.on("data",function (data) {
      //     console.log(data);
      // });
      process.stdin.on("readable",function () {
          var data=process.stdin.read();
          //回调函数没有参数 需要通过process.stdin.read来读取用户的键盘输入信息
          console.log(data);
      });

      //exit事件
      process.on("exit",function () {
          console.log("programe will exit");
      });
      //在程序正常退出的之前  会触发exit事件

      //SIGINT --> signal    interrupted  信号 被中断
      //当一个信号被中断的时候就会触发SIGINT事件(cmd 中  ctrl+c会中断信号)

      process.on("SIGINT",function () {//会改变程序默认的退出行为
          console.log("programe has a sigint");
          process.exit();//让程序正常退出
      });
      ```

  - 3. `console`：指向`Node`内置的`console`模块，提供命令行环境中的标准输入、标准输出功能。

        通常是写`console.log()`;

#### 全局函数

- 1. 定时器函数：共有4个，分别是`setTimeout()`, `clearTimeout()`, `setInterval()`, `clearInterval()`。
- 2. `require`：用于加载模块

#### 全局变量：

- 1. `_filename`：指向当前运行的脚本文件名。
- 2. `_dirname`：指向当前运行的脚本所在的目录

#### 准全局变量

- 模块内部的局部变量，指向的对象根据模块不同而不同，但是所有模块都适用，可以看作是伪全局变量，主要为`module`, `module.exports`, `exports`等。

- `module`变量指代当前模块。`module.exports`变量表示当前模块对外输出的接口，其他文件加载该模块，实际上就是读取`module.exports`变量。

- `module.id` 模块的识别符，通常是模块的文件名。
- `module.filename` 模块的文件名。
- `module.loaded` 返回一个布尔值，表示模块是否已经完成加载。
- `module.parent` 返回使用该模块的模块。
- `module.children` 返回一个数组，表示该模块要用到的其他模块。

- 这里需要特别指出的是，`exports`变量实际上是一个指向`module.exports`对象的链接，等同在每个模块头部，有一行这样的命令。
`var exports = module.exports;`
- 这造成的结果是，在对外输出模块接口时，可以向`exports`对象添加方法，但是不能直接将`exports`变量指向一个函数：
`exports = function (x){ console.log(x);};`
- 上面这样的写法是无效的，因为它切断了`exports`与`module.exports`之间的链接。
- 如果你觉得，`exports`与`module.exports`之间的区别很难分清，一个简单的处理方法，就是放弃使用`exports`，只使用`module.exports`。

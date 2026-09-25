---
# 必填。项目名称。
title: "JS中的caller和callee"
# 可选，和文章一样使用。
slug: JS中的caller和callee
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-26
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "JS中的caller和callee"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Javascript
tags:
  - Javascript
  - JS
  - caller
  - callee
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

### `caller`

- 检验函数被谁调用过
- 检验函数被谁调用过 返回值是调用这个函数的函数本身,没有的话返回null
<!-- more -->

### `arguments.callee`

- 函数本身

```js
function Fn() {
    console.log(arguments.callee.caller);//-->function fn() {Fn()}
    //-->arguments.callee 函数本身
    //caller:检验函数被谁调用过 返回值是调用这个函数的函数本身,没有的话返回null
    console.log(Fn.prototype.constructor === arguments.callee);//-->true
}
function fn() {
    Fn()
}
fn();
```

```js
function sum(n) {
    console.log(arguments.callee===arguments.callee.caller);
    //->第一次输出false，因为第一次是函数自己执行，即自调用 自调用的时候console.log(arguments.callee.caller) 输出null   而此时arguments.callee 函数本身仍然是sun函数本身   所以输出false;
    // -->当自调用执行完成后  arguments.callee===arguments.callee.caller===sum这个函数本身   --->  返回true
    if(n<=0){
        return 0
    }
    return n+sum(--n);
}
console.log(sum(10));//55
```

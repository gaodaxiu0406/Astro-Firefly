---
# 必填。项目名称。
title: "JS函数内部的[[scope]]属性"
# 可选，和文章一样使用。
slug: JS函数内部的[[scope]]属性
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-09-05
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "JS函数内部的`[[scope]]`属性"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Javascript
tags:
  - Javascript
  - JS
  - scope
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

### `[[scope]]`

函数内部的`[[scope]]`属性是虚拟出来的一个属性，我们实际访问时访问不到这个属性的，这个属性是为了让我们更好的理解函数，虚拟出来的一个属性。

<!-- more -->
```js
var fun1,fun2;
function foo() {
    var x = 10;
    fun1 = function () {
        console.log(++x);//11  x=11
    };
    fun2 = function () {
        console.log(--x);//10  x=10
    }
}
foo();   // 初始化了fun1,fun2函数
fun1();  // 11
fun2();  // 10
```

- 产生这个情况的原因是:在同一父作用域中的闭包共同同一个`[[scope]]`属性

```js
var x = 10;
function foo () {
    console.log(x);
}
foo(); // 10
function fun () {
    var x = 20;
    var foo1 = foo;
    foo1();   // 10
}
fun();
```

- 是10的原因就是在复制函数的时候，复制后的函数与复制前的函数引用的是同一个`[[scope]]`属性，由于`foo`的`[[scope]]`属性中的`x`是保存在函数父作用域链中的，这个也就是指的全局的变量对象（也就是全局变量）中的`x`，`foo1`中`[[scope]]`属性与`foo`的相同，所以`foo1`在执行创建的`scope`，只有`foo1`内部的`[[scope]]`属性（也就是`foo`内部的`[[scope]]`属性），所以在查找原型链时，`foo1`作用域链就直接查找到了全局对象中的`x`属性，所以会返回10。

- `[[Scope]]`和执行期上下文虽然保存的都是作用域链，但不是同一个东西

- `[[Scope]]`属性是函数创建时产生的，会一直存在;而执行上下文在函数执行时产生，函数执行结束便会销毁

- 伪代码:`foo`函数创建产生`[[Scope]]`对象

```js
foo.[[Scope]] = {
    GO: {
        this: window ,
        window:... ,
        document: ... ,
        a: undefined, //预编译阶段还不知道a的值是多少，执行过程中会修改
        foo: function(){...},
        ......
    }
}
```

> 详细了解推荐地址:[http://www.2cto.com/kf/201312/263748.html](http://www.2cto.com/kf/201312/263748.html)

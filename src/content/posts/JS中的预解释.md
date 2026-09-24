---
# 必填。项目名称。
title: "JS中的预解释"
# 可选，和文章一样使用。
slug: JS中的预解释
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-04-29
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "JS中的预解释"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Javascript
tags:
  - Javascript
  - JS
  - 预解释
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

### 预解释的基础知识
<!-- more -->

例子:

```js
console.log(d);//-->function d(){};
d=1;//-->d=1
s=d;//-->s=1
function d(){//-->xxxfff000

}
d();//-->d is not a function
```

- 1.预解释:

    是一个过程，作用域形成之后，代码执行之前，把所有带`var`关键字和`function`提前声明或定义。

- 2.作用域：

  1) 全局作用域：`window`下，一打开浏览器就会形成。
  2) 私有作用域：一个函数就是一个私有作用域，函数一执行就会形成私有作用域。

- 3.声明:

    告诉浏览器这里有个变量，`var`关键字的只有声明。

- 4.定义:

    赋值过程，在预解释的时候`function`即声明还定义。

- 5.注意:

    预解释的时候遇到变量已经声明过了就不用声明了，但是需要重新定义,例如:

    ```js
    //变量只声明未定义就是undefined
    console.log(obj1);//-->undefined
    var obj1={name:"111"};
    console.log(fn);
    function fn() {}
    // 1. 全局作用形成
    // 2. 全局作用域下的预解释：var obj1，function fn=xxxfff000
    // 3. 代码执行：
        // 1.console.log(obj1);-->undefined
        // 2.obj1=xxxfff111
        // 3. console.log(fn);-->function fn() {}
    ```

### 预解释的几种特殊情况

> 注意: 全局作用域下的变量就是window的一个属性

#### 1.`=`右边函数不进行预解释

函数作为值的时候,绑定事件的时候,不进行预解释,如下：

```js
var ff=function () {
    console.log(1);
};
```

#### 2.`return`后面的代码不执行但是需要预解释

return出的内容执行但是不进行预解释:

```js
function fn() {
    var a=0;
    console.log(f);//function f(){}
    return function () {
        console.log(1);
        return 1
    };
    function f() {}
}
var d=fn();
console.log(d());
fn()();
```

#### 3.在条件语句中

1) 不管条件是否成立都进行预解释

```js
    console.log(num);
    if (0){
        //虽然条件不成立 但是需要预解释
        var num=0
    }
    ss=0;//->window.ss=0
    console.log("ss" in window);
```

2) 条件中有函数`function`

    在条件中的`var`和`function`只声明不定义，声明的时候当遇到变量已经被声明了，就会报错。

    ```js
    if('a' in window){
    var a=1;
    function(){};//-->'a' has already been declared
    }
    ```
  
    条件一旦成立，首先给函数赋值

    ```js
        console.log(a);
        if ("a" in window){
            console.log(a);
            a=1;
            function a() {}
            console.log(a);
        }
        //预解释：function a  -->就相当于给window增加一个“a”属性
        //"a" in window 就是true
        //条件成立第一步先给function a赋值=xxxfff000
        //代码执行：console.log(a);xxxfff000->function a() {}
        // a=1,重新给a赋值

    ```

#### 4.自执行函数 不进行预解释

```js
//console.log(sss)
;(function  sss() {
    console.log("a")
})();
```

#### 5.函数作为参数的时候不进行预解释

```js
[1,2,3].sort(function(a,b){
return a-b;
});
```

#### 6.预解释的时候遇到已经声明过得变量不需要声明了，但是需要定义

```js
var s1=1;
function s1() {//s1=xxxfff000
    console.log("s1")
}
function s1() {//s1=xxxfff111
    console.log("s11")
}
console.log(s1);
```

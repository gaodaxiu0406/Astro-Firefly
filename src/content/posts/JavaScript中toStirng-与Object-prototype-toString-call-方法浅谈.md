---
# 必填。项目名称。
title: "JavaScript中toStirng()与Object.prototype.toString.call()方法浅谈转载"
# 可选，和文章一样使用。
slug: JavaScript中toStirng()与Object.prototype.toString.call()方法浅谈转载
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-09-09
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "JavaScript中toStirng()与Object.prototype.toString.call()方法浅谈转载"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Javascript
tags:
  - JavaScript
  - JS
  - toStirng()
  - Object.prototype.toString.call()
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
- 一、toString()是一个怎样的方法？它是能将某一个值转化为字符串的方法。然而它是如何将一个值从一种类型转化为字符串类型的呢？
通过下面几个例子，我们便能获得答案：
<!-- more -->
    - 1.将boolean类型的值转化为string类型：
    ```js
    console.log(true.toString());//"true"
    console.log(false.toString());//"false"
    ```

    - 2.将string类型按其字面量形式输出：
    ```js
    var str = "test123y";
    console.log(str.toString());//"test123y"
    ```

    - 3.将Object类型转化成string类型（JavaScript原生的Array类型、Date类型、RegExp类型以及Number、Boolean、String这些包装类型都是Object的子类型）：
自定义Object类型（没有重新定义toString方法）：
    ```js
    var obj = {name:"Tom", age:18};
    console.log(obj.toString());//"[object Object]"此时调用的是从Object继承来的原始的toString()方法
    ```

- 接下来的三个例子都是以重写的方式实现了toString()方法；
    - 1.Array类型：
    ```js
    var arr = ["tom",12,"rose",18];
    console.log(arr.toString());//"tom,12,rose,18"
    ```
    - 2.RegExp类型
    ```js
    var patten = new RegExp("\\[hbc\\]at", "gi");
    console.log(patten.toString());//"/\[hbc\]at/gi"
    ```
    - 3.Date类型
    ```js
    var date = new Date(2014,02,26);//注意这种格式创建的日期，其月份是3月
    console.log(date.toString());//"Wed Mar 26 2014 00:00:00 GMT+0800"输出格式因浏览器不同而不同，此为firefox的输出格式；
    ```
    - 4.Number类型也是以重写的方式实现toString()方法的，请看以下例子：
        - (1)它可以接受一个整数参数，并将调用这个方法的数值转化成相应进制的字符串：
        ```js
        var num = 16;
        console.log(num.toString(2));//10000 二进制
        console.log(num.toString(8));//20 八进制
        console.log(num.toString(16));//10 十六进制
        console.log(num.toString(5));//31 虽然没有五进制，但是这样传参是可以被toString()方法接受的
        ```
        - (2)再看下面的代码：
        ```js
        console.log(1.toString());//这种写法会报错语法错误，但是下面的写法都是合法的；
        console.log((1).toString());//"1"
        console.log(typeof (1).toString());//string
        console.log(1..toString());//"1"
        console.log(typeof (1).toString());//string
        console.log(1.2.toString());//"1"
        console.log(typeof (1).toString());//string
        ```
        - 这是因为javascript引擎在解释代码时对于“1.toString()”认为“.”是浮点符号，但因小数点后面的字符是非法的，所以报语法错误；
        - 而后面的“1..toString()和1.2.toStirng()”写法，javascript引擎认为第一个“.”小数点，的二个为属性访问语法，所以都能正确解释执行；
        - 对于“(1).toStirng()”的写法，用“()”排除了“.”被视为小数点的语法解释，所以这种写法能够被解释执行；
        - (3)纯小数的小数点后面有连续6或6个以上的“0”时，小数将用e表示法进行输出；
        ```js
        var num = 0.000006;//小数点后面有5个“0”
        console.log(num.toString());//"0.000006"
        var num = 0.0000006;//小数点后面有6个“0”
        console.log(num.toString());//"6e-7"
        ```
        - (4)浮点数整数部分的位数大于21时，输出时采用e表示法；
        ```js
        var num = 1234567890123456789012;
        console.log(num.toString());//"1.2345678901234568e+21"
        ```
    - 看到这里大家难免会有些疑问，这些基本的数据类型的值都是常量，而常量是没有方法的，为什么能够调用方法呢？答案是这样的，五种基本类型除了null、undefined以外都有与之对应的特殊的引用类型——包装类型。当代码被解释执行时，底层会对基本类型做一个类型转换，即将基本类型转换成引用类型，这样就可以调用相应引用类型有权访问到的方法。

- 二、toString()方法定义在何处？
- 运行以下代码：
```js
var pro = Object.prototype;
var pr = pro.__proto__;//ie11之前版本不支持该属性
console.log(typeof pro);//"object"
console.log(String(pro));//"[object Object]"
console.log(pro.hasOwnProperty("toString"));//true
console.log(typeof pr);//"object"
console.log(String(pr));//"null"
console.log(pr.hasOwnProperty("toString"));//报错
```
- 由此可知，toString()定义在Object.prototype上；

- 三、使用Object.prototype上的原生toString()方法判断数据类型，使用方法如下：
Object.prototype.toString.call(value)
    - 1.判断基本类型：
    ```js
    Object.prototype.toString.call(null);//”[object Null]”
    Object.prototype.toString.call(undefined);//”[object Undefined]”
    Object.prototype.toString.call(“abc”);//”[object String]”
    Object.prototype.toString.call(123);//”[object Number]”
    Object.prototype.toString.call(true);//”[object Boolean]”
    ```
    - 2.判断原生引用类型：
    - 函数类型
    ```js
    Function fn(){console.log(“test”);}
    Object.prototype.toString.call(fn);//”[object Function]”
    ```

    - 日期类型
    ```js
    var date = new Date();
    Object.prototype.toString.call(date);//”[object Date]”
    ```

    - 数组类型
    ```js
    var arr = [1,2,3];
    Object.prototype.toString.call(arr);//”[object Array]”
    ```

    - 正则表达式
    ```js
    var reg = /[hbc]at/gi;
    Object.prototype.toString.call(arr);//”[object Array]”
    ```

    - 自定义类型
    ```js
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    var person = new Person("Rose", 18);
    Object.prototype.toString.call(arr); //”[object Object]”
    ```

    - 很明显这种方法不能准确判断person是Person类的实例，而只能用instanceof 操作符来进行判断，如下所示：
    ```js
    console.log(person instanceof Person);//输出结果为true
    ```
    - 3.判断原生JSON对象：
    ```js
    var isNativeJSON = window.JSON && Object.prototype.toString.call(JSON);
    console.log(isNativeJSON);//输出结果为”[object JSON]”说明JSON是原生的，否则不是；
    ```js
    - 注意：Object.prototype.toString()本身是允许被修改的，而我们目前所讨论的关于Object.prototype.toString()这个方法的应用都是假设toString()方法未被修改为前提的。
    - 本文所讨论内容多参考于《JavaScrip高级编程》第三版，另因个人水平有限，如有描述不当之处还请高手指正。

##### 原文链接`http://www.jianshu.com/p/5c6503279685`
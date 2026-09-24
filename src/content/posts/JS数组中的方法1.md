---
# 必填。项目名称。
title: "JS数组中的方法1"
# 可选，和文章一样使用。
slug: JS数组中的方法1
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2018-04-25
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "JS数组中的方法1:charCodeAt、push、unshift、splice、pop、shift、slice、concat、indexOf、lastIndexof、forEach、map、join、toString、reverse、sort"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Javascript
tags:
  - JavaScript
  - JS
  - charCodeAt
  - push
  - unshift
  - splice
  - pop
  - shift
  - slice
  - concat
  - indexOf
  - lastIndexof
  - forEach
  - map
  - join
  - toString
  - reverse
  - sort
  - 数组方法
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
## 数组中的方法
- 1.给数组添加值
2) charCodeAt（索引） 返回结果对应的是ASCII码;原字符串不变
<!-- more -->
    - 1). push();向数组末尾增加n项
        - 参数:想向数组末尾增加的内容,可以传递多个值,统一向数组末尾增加n向
        - 返回值:新增后数组的长度
        - 原数组:改变
    ```
    var ary=[12,23,34,45];
        ary.push(56);
        console.log(ary);//-->[12,23,34,45,56]
    ```
    - 2). unshift();向数组开头增加n项
        - 参数:想向数组开头增加的内容,可以传递多个值,统一向数组开头增加n向
        - 返回值:新增后数组的长度
        - 原数组:改变

- 扩展:向数组末尾增加
    - a). splice(a.length,0,x);向末尾增加,可增加多项

- 2.删除数组中的项
    - 1). pop();删除数组最后一项内容
        - 参数:没有
        - 返回值:被删除的那一项内容
        - 原数组:改变
    - 2). shift();删除数组中的第一项
        - 参数:没有
        - 返回值:被删除的那一项内容
        - 原数组:改变

- 扩展:删除数组最后一项内容的方法
    - a) pop();删除数组最后一项内容
    - b) ary.length--;
    - c) ary.splice(ary.length-1);


- 3.数组中的截取和拼接
    - 1).slice 实现数组的截取，在原来的数组中截取某一部分
        - a). slice(n,m);
        - a1). n>=m 返回空数组
        - a2). n<0,m<0,n<m 从索引m开始找到索引为n处，不包含n，将找到的部分，以新数组返回，原数组不变。原数组的索引最后一位是0,倒数第二位索引是-1,以此类推;例如:
        ```
        var ary1=[11,22,33,44,55,66,77,88,99];
        var res=ary1.slice(-4,-3);
        console.log(res,ary1);
        //[66]   (9) [11, 22, 33, 44, 55, 66, 77, 88, 99]
        ```
        - a3). n>0,m<0  原数组的长度（从前往后）变为总长度+m(m为负数，即原数组总长度减短)，slice(n,m)返回索引n开始到减短后的数组末尾  当n和m的绝对值相加>=原数组总长度时，slice(n,m)返回空数组;例如
        ```
        var ary1=[11,22,33,44,55,66,77,88,99];
        var res=ary1.slice(3,-3);
        //[44, 55, 66]   (9) [11, 22, 33, 44, 55, 66, 77, 88, 99]
        ```
        - a4). n>0,m>0,m>n
             参数:从索引n开始找到索引m处(不包含m);
             返回值:索引n项到索引m-1项,将找到的部分以新数组返回;
             原数组:不变;
        - b). slice(n);
            - 参数:从索引n开始一直找到数组末尾
            - 将找到的部分以新数组返回
            - 原数组:不变
        - c). slice(0);/slice()
            - 把原来的数组克隆一份一模一样的新数组返回
            - 原数组:不变
    - 2).concat();把两个数组拼接在一起
    - 参数:
        - a). ary1.concat(ary2);将ary1和ary2进行拼接,ary2在后面
        - b). ary1.concat();把ary1克隆一份一模一样的数组
    - 原数组:不变

- 4.修改数组中某一项的值
    - 1).利用对象的操作方式修改某一项的值,例如:ary[2]=100;
        - 原数组:改变
    - 2).数组中的方法splice
        - a). splice 既能实现删除,也能实现增加,还能实现修改

        splice的删除:
        - 返回值:删除的数据以新数组的方式返回
        - 原数组:改变
        - a1). splice(n,m);从索引n开始,删除m个元素,把删除的内容以一个新数组的方式返回,原数组改变
        - a2). splice(n);从索引n开始,删除到数组的末尾
        - a3). splice(0);从索引0开始,删除到数组的末尾;原数组返回空数组,splice(0)相当于克隆一份原数组,这样的克隆会修改原来的数;例如:
        ```
        var a=[11,22,33,44,55,66,77];
        var res=a.splice(0);
        console.log(res,a);
        //(7) [11, 22, 33, 44, 55, 66, 77] , []
        ```
        - a4). splice();相当于没有对原数组进行任何操作,splice()返回一个空数组.原数组不变;例如:
```
    var a=[11,22,33,44,55,66,77];
var res=a.splice();
console.log(res,a);
//[] , (7) [11, 22, 33, 44, 55, 66, 77]
```
        - a5). splice(a.length-1);删除最后一项，把所有索引最后一个删除掉;例如:
    ```
    var a=[11,22,33,44,55,66];
    var res=a.splice(a.length-1);
    console.log(res,a);
    //[66] , (5) [11, 22, 33, 44, 55]
    ```

    splice的修改:
    - b1). splice(n,m,x); 从索引n开始，删除m个，用x替换删除的部分,x可以是多项;例如:
    ```
    var b=[1,2,3,4,5,6];
        var res=b.splice(1,2,11,12,13);
        console.log(res,b);
        //[2, 3] , (7) [1, 11, 12, 13, 4, 5, 6]
    ```

    splice的增加:
    - c1). splice(n,0,x); 从索引n开始，删除0个，用x替换删除的部分-->相当于把x增加到索引n的前面;例如:
    ```
    var a=[11,22,33,44,55,66];
    var res=a.splice(1,0,77,88);
    console.log(res,a);
    //[] , (8) [11, 77, 88, 22, 33, 44, 55, 66]
    ```
    - c2). splice(a.length,0,x);向末尾增加,可增加多项

- 5.通过属性值查找索引:只有在标准浏览器下兼容的(数组中不兼容 字符串中兼容)原数组不变
    - 1) indexOf()
    - 2) lastIndexof()
- 6.遍历数组中的每一项
    - 1) forEach(function(x,y,i){});没有返回值,例如:
    ```
    var b=[11,22,33,44,55,66,11];
    b.forEach(function (item,index) {
        //item为数组当前项,index为数组中的索引
        console.log(item,index);
    });
    //没有返回值
       var new1b=b.forEach(function (a,b) {
               return a*10;
           });
           console.log(new1b);//undefined
    ```
    - 2) map(function(x,y,i){return;});
    ```
    var b=[11,22,33,44,55,66,11];
    b.map(function (item,index) {
        //item为数组当前项,index为数组中的索引
        console.log(item,index);
    });
    var newb=b.map(function (item,index) {
        return item*10;
    });
    console.log(newb);//[110, 220, 330, 440, 550, 660, 110]
    ```

- 7.将数组转化为字符串:
    - 1) join("");按照每一个分隔符，把数组中的每一项拼接成一个字符串
    ```
    var b=[12,22,33,44,55];
    var res=b.join('+');
    console.log(res,b);
    //"12+22+33+44+55"  (5) [12, 22, 33, 44, 55]
    //扩展:eval：JS中把字符串变为JS表达式执行的一种方法
        console.log(eval(res));//166
        //简写:
        console.log(eval(b.join('+')));//166
    ```
    - 2) toString();原数组不变
    ```
        var b=[12,22,33,44,55];
        var res=b.toString();
        console.log(res);//"12,22,33,44,55"
    ```
- 8.排序
    - 1) reverse();把数组倒过来排列,原数组也倒过来排列;例如:
    ```
        var b=[11,22,33,44,55,66,11];
        var res=b.reverse();
        console.log(res,b);
        //(7) [11, 66, 55, 44, 33, 22, 11]   (7) [11, 66, 55, 44, 33, 22, 11]
    ```
    - 2) sort();给数组进行排序,原数组也进行排序
        - a). ary.sort(); 只能处理10以内的数字
        - b). sort(function(a,b){return a-b;});从小到大排序
        - c). sort(function(a,b){return b-a;);从大到小排序

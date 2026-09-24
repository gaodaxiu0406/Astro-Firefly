---
# 必填。项目名称。
title: "JS数组中的方法2"
# 可选，和文章一样使用。
slug: JS数组中的方法2
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2018-08-20
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "JS数组中的方法2:forEach、filter、map、some、every、reduce、includes(es6)、find(es6)"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Javascript
tags:
  - JavaScript
  - JS
  - forEach
  - filter
  - map
  - some
  - every
  - reduce
  - includes
  - find
  - 数组方法
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
## 保证node的版本
```angular2html
node -v //查询node版本
```
- 最好升级到8.5以上版本
<!-- more -->

## 编译器
- webstorm版本>2017以上版本
- vscode
- sublime

## webstorm配置npm和语法
- File->Setting中配置 每打开一个项目都要重新配置
- File->Default Setting 中配置后 以后就不用配置了
  - react jsx 语法是支持react的语法 包含es6语法 可以直接使用jsx语法

### 1.forEach(没有返回值)
```
let arr=[1,2,3,4,5]
for(let i=0;i<arr.length;i++){//纯编程的 编程式语法:自己调用循环 可以很明确的看出来代码怎么执行的
  console.log(arr[i])
}
arr.forEach(function(item){//声明式语法 好处:不关心如何实现 不支持return，不管写不写return都会执行完
  console.log（item）
},改变this指向)
```
- 面试题:forEach，for in，for，for of的区别（为什么遍历数组的时候  不采用for in）
  - 按理说 索引应该是数字number数据类型的，但是for in循环中key会变成string字符串数据类型

  ```
    for(let key in arr){
      console.log(typeof key) //string  包括数组的私有属性也能打印出来
    }
  ```
  - 如果给arr加上个属性 arr.b='100'  属于数组的私有属性  for in可以打印出来
  ```
    for(let val of arr){//支持return 并且是val（值）of数组（不能遍历对象）

    }
  ```

> 总结:
  - forEach不支持return
  - for in循环遍历出来的包含私有属性
  - for of 既能return（并且是val（值）of数组），又能遍历私有属性（不能遍历对象）
    > 扩展: 遍历对象的方法:Object.keys ->将对象的key做成一个新的数组
    ```
    let obj={a:1,b:2}
    //[a,b]
    for(let val of Object.keys(obj)){
       console.log(val)// a        b
       console.log(obj[val])// 把val变成变量 只能用[],不能用点，点会把val变成字符串，就取不出来了
    }
    ```




### 2.filter （过滤）- 删除
- 是否操作原数组:no
- 这个方法的返回结果:过滤后的新数组
- 回调函数的返回结果:
  - 返回true表示这一项放到新数组中
  - 返回false表示这一项不放到新数组中
> 过滤出数组中大于2小于5的数
- 错误示范
```
let arr=[1,2,3,4,5].filter(function(item,index)){
  return 2<item<5 //-->不行  会先比较前面2<item  永远都是true  会输出[1,2,3,4,5]
}
console.log(arr) //[1,2,3,4,5]
```
- 正确示范
```
let arr=[1,2,3,4,5].filter(function(item,index)){
  return item>2&&item<5
}
console.log(arr) //[3,4]
```

### 3.map(映射)  - 更新
- 将原有的数组 映射成新数组
- 是否操作原数组:no
- 这个方法的返回结果:返回新数组
- 回调函数的返回结果:回调函数中返回什么，这一项就是什么
> 举例:有一个数组[1,2,3],如何将他变成
```
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
</ul>
- 思路:
let arr=[1,2,3].map(function(item){
   return 2
})
console.log(arr)//[2,2,2]
let arr1=[1,2,3].map(function(item){
   return item*=3
})
console.log(arr1)//[3,6,9]
- 实现功能:es6中的模板字符串拼 ${}中间包变量
let arr2=[1,2,3].map(function(item){
   return `<li>${item}</li>` //是es6中的模板字符串，遇到变量用${}取值
})
console.log(arr2)//[<li>1</li>,<li>2</li>,<li>3</li>]
console.log(arr2.join(''))//<li>1</li><li>2</li><li>3</li>
```

> 总结:
- 如果想删除数组中的某一项，可以用filter
- 如果想更新或者修改某个数组，可以用map

## 4.includes (是否包含)
> 数组中只要有5就拿出来
```
let arr=[1,2,3,4,55]
arr.includes(5) //false  返回的是布尔类型 有5就是true，没有5就是false  很局限
```
## 5.find
- 返回找到的那一项
- 不会改变原数组
- 回调函数中:
    - 返回true表示找到了，找到后停止循环
    - 返回undefined表示没找到
> 数组中只要包含5就拿出来
```
let arr=[1,2,3,4,55,555]
let newArr=arr.find(function(item,index){
  return item.toString().indexOf(5)>-1  //找到了
})
console.log(newArr)  //55
```

> 总结:
- 找到具体的某一项,用find。实际应用中:比如有用户列表，用户都有自己的用户名和密码，拿到用户的密码对应找到用户的用户名，找到一个就会停止往下找。

## 6.some
- 找true，找到true后停止,返回true;找不到返回false。

## 7.every
- 找false，找到false后停止,返回false

> 判断一个数组中有没有5,用some
```
let arr=[1,2,3,4,55,555]
let newArr=arr.some(function(item,index){
  return item.toString().indexOf(5)>-1  //找到了
})
console.log(newArr)  //true
```

## 8.reduce(收敛)
- 四个参数:prev上一个、next下一个、index索引、item原数组
- 返回的结果:叠加后的结果
- 回调函数返回的结果:
- 原数组不变

> 求数组中的和
```
//第一步分析:
[1,2,3,4,5].reduce(function(prev,next,index,item){
    console.log(arguments)
    //{'0':1,'1':2,'2':1,'3':[1,2,3,4,5]}->prev数组的第一项,next数组的第二项
    //{'0':undefined,'1':3,'2':2,'3':[1,2,3,4,5]}->prev是undefined,next数组的第三项
    //{'0':undefined,'1':4,'2':3,'3':[1,2,3,4,5]}->prev是undefined,next数组的第四项
    //{'0':undefined,'1':5,'2':4,'3':[1,2,3,4,5]}->prev是undefined,next数组的第五项
    //-->prev是undefined的原因，因为这里没有return
})
//第二步分析->有return的时候:
[1,2,3,4,5].reduce(function(prev,next,index,item){
    console.log(arguments)
    return 100 //本次的返回值会作为下一次的prev
    //{'0':1,'1':2,'2':1,'3':[1,2,3,4,5]}->prev数组的第一项,next数组的第二项
    //{'0':100,'1':3,'2':2,'3':[1,2,3,4,5]}->prev是100,next数组的第三项
    //{'0':100,'1':4,'2':3,'3':[1,2,3,4,5]}->prev是100,next数组的第四项
    //{'0':100,'1':5,'2':4,'3':[1,2,3,4,5]}->prev是100,next数组的第五项
})
//求和:
let sum=[1,2,3,4,5].reduce(function(prev,next,index,item){
    console.log(prev,next)
    return prev+next
})
console.log(sum) //15
```

> 求30*2+30*3+30*4
```
//思路:
let sum2=[{price:30,count:2},{price:30,count:3},{price:30,count:4}].reduce(function(prev,next){
    return prev.price*prev.count+next.price+next.count
    //30*2+30*3  ->150
    //150.price*150.count + ...  ->NaN
})
console.log(sum2) //NaN
//在数组最前面加上0 会导致多循环一次
let sum2=[0,{price:30,count:2},{price:30,count:3},{price:30,count:4}].reduce(function(prev,next){
    return prev+next.price+next.count
    //0+30*2  ->60
    //60+30*3  ->150
    //150+30*4 ->270
})
console.log(sum2) //270
//传第二个参数0来解决 -> 默认指定第一次的prev
let sum2=[{price:30,count:2},{price:30,count:3},{price:30,count:4}].reduce(function(prev,next){
    return prev+next.price+next.count
    //0+30*2  ->60
    //60+30*3  ->150
    //150+30*4 ->270
},0)
console.log(sum2) //270
```

> 总结:求和、求叠加、两个数组合成一个数组，可以用reduce

> 扩展
- 数组扁平化:将一个二维数组变为一维数组怎么写？可以使用reduce -> 将`[[1,2,3],[4,5,6],[7,8,9]]变为[1,2,3,4,5,6,7,8,9]`
```
let arr=[[1,2,3],[4,5,6],[7,8,9]].reduce(function(prev,next){
    return prev.concat(next)
})
console.log(arr)//[1,2,3,4,5,6,7,8,9]
```



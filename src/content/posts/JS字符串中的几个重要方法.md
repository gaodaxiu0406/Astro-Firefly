---
# 必填。项目名称。
title: "字符串中的几个重要方法"
# 可选，和文章一样使用。
slug: Javascript字符串中的几个重要方法
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-02
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "Javascript字符串中的几个重要方法：charAt、charCodeAt、substr、subString、slice、indexOf、lastIndexOf、toUpperCase、toLowerCase、replace、split"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Javascript
tags:
  - Javascript
  - JS
  - charAt
  - charCodeAt
  - substr
  - subString
  - slice
  - indexOf
  - lastIndexOf
  - toUpperCase
  - toLowerCase
  - replace
  - split
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

## 1.通过索引查找字符串

### 1.1 `charAt`(索引) 字符串上的`charAt`方法里边传索引值，进行搜索指定索引位置的字符，还是字符串格式;原字符串不变。

### 1.2 `charCodeAt`（索引） 返回结果对应的是`ASCII`码;原字符串不变。

<!-- more -->
例如:

```js
var str = 'addias';
console.log(str.charAt(0),str);
//"a" "addias" 原字符串不变
console.log(str.charCodeAt(0),str);
//97 "addias"  原字符串不变
```

## 2.检取字符串

### 2.1 `substr`

#### 2.1.1 `substr(n,m)`; 从索引n开始截取m个

- 返回值为截取的字符串
- 原有字符串不变

```js
    var str = 'addias';
    console.log(str.substr(1, 2),str);//"dd" "addias"
```

#### 2.1.2 `str.substr()` / `str.substr(0)`  复制字符串

```js
var str = 'addias';
console.log(str.substr(),str);
//"addias" "addias" 复制字符串
console.log(str.substr(0),str);
//"addias" "addias" 复制字符串
```

### 2.2 `subString`

#### 2.2.1 `subString(n,m)` 从索引n找到索引m之前，不包含m处;原字符串不变

```js
var str = 'addias';
console.log(str.substring(3, 4),str);
//"i" "addias"
```

#### 2.2.1 `substring()` / `substring(0)` 克隆字符串

```js
var str = 'addias';
console.log(str.substring(0),str);
//"addias" "addias"
console.log(str.substring(),str);
//"addias" "addias"
```

### 2.3 `slice`

字符串也可以使用`slice`

```js
var str = 'addias';
console.log(str.slice(-1+str.length));//s
console.log(str.slice(-1)); //s 同数组的使用方法一样
console.log(str.slice(-2)); //as 同数组的使用方法一样
```

### 2.4 `indexOf` / `lastIndexOf`

`indexOf`字符串中当前字符出现的第一个索引;
`lastIndexOf`字符串中当前字符出现的最后一个索引;

```js
var str = 'addias';
console.log(str.indexOf('f'));//-1
console.log(str.lastIndexOf('a'));//4
```

### 2.5 `toUpperCase` / `toLowerCase`

`toUpperCase`字符串转化成大写;
`toLowerCase`字符串转化成小写;

```js
var str = 'addias';
console.log(str.toUpperCase(), str);
// "ADDIAS" "addias" 字符串转化成大写
var str = 'ADDIAS';
console.log(str.toLowerCase(), str);
//"addias" "ADDIAS" 字符串转化成小写
```

### 2.6 `replace`

replace 替换字符串中的字符;原字符串不变。

```js
var str1 = '我,爱,中,国';
console.log(str1.replace('我', 'wo'), str1);
// "wo,爱,中,国"    "我,爱,中,国"
```

### 2.7 `split`

`split` 将字符串拆分成数组;将字符串以字符串中存在的指定分隔符拆分成数组

```js
var str1 = '我,爱,中,国';
var str2 = 'sdasdasdasdasd';
console.log(str2.split('a'));
//(5) ["sd", "sd", "sd", "sd", "sd"]
console.log(str2.split());
//["sdasdasdasdasd"]
console.log(str1.split(','));
//["我", "爱", "中", "国"]
console.log(str1.split(''));
//["我", ",", "爱", ",", "中", ",", "国"]
```

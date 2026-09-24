---
# 必填。项目名称。
title: "ios和android 浏览器适配问题总结"
# 可选，和文章一样使用。
slug: ios和android 浏览器适配问题总结
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-09-03
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "ios和android 浏览器适配问题总结"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: 浏览器适配
tags:
  - CSS
  - 手机浏览器适配
  - Ios
  - Android
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
## 1.防止手机中网页放大和缩小
```html
<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0,user-scalable=0" />
```
<!-- more -->
## 2.安卓浏览器看背景图片,有些设备会模糊?
- 用同等比例的图片在PC机上很清楚，但是手机上很模糊，原因是什么呢？
    - 经过研究,发现是devicePixelRatio作怪，因为手机分辨率太小，如果按照分辨率来显示网页，这样字会非常小，所以苹果当初就把iPhone 4的960*640分辨率，在网页里只显示了480*320，这样devicePixelRatio＝2。现在android比较乱，有1.5的，有2的也有3的。 想让图片在手机里显示更为清晰，必须使用2x的背景图来代替img标签（一般情况都是用2倍）。
    - 例如一个div的宽高是100，背景图必须得宽高是200，然后background-size:contain;这样显示出来的图片就比较清晰了。
```css
background:url(../images/icon/all.png) no-repeat center center;
-webkit-background-size:50px 50px;
background-size: 50px 50px;
display:inline-block;
width:100%;
height:50px;
```

## 3.一些情况下对非可点击元素(如label/span)监听click事件，ios下不会触发
- 解决方案:css增加cursor:pointer;

## 4.在ios和andriod中,audio元素和video元素无法自动播放
- 这个不是 BUG，由于自动播放网页中的音频或视频，会给用户带来一些困扰或者不必要的流量消耗，所以苹果系统和安卓系统通常都会禁止自动播放和使用 JS 的触发播放，必须由用户来触发才可以播放。
- 解决方法思路:先通过用户 touchstart 触碰,触发播放并暂停(音频开始加载,后面用 JS 再操作就没问题了)。
```js
document.addEventListener('touchstart',function() {
      document.getElementsByTagName('audio')[0].play();
      document.getElementsByTagName('audio')[0].pause();
});
```

## 5.fixed定位缺陷
- ios下fixed元素容易定位出错，软键盘弹出时，影响fixed元素定位, android下fixed表现要比iOS更好，软键盘弹出时，不会影响fixed元素定位 , ios4下不支持position:fixed;
- 解决方案:可用iScroll插件解决这个问题

## 6.Input的placeholder会出现文本位置偏上的情况
- PC端设置line-height等于height能够对齐，而移动端仍然是偏上
- 解决方案:设置line-height:normal;

## 7.圆角bug
- 某些Android手机圆角失效
- 解决方案:
```css
background-clip:padding-box;
```

## 8.IOS中input键盘事件keyup、keydown、keypress支持不是很好
- 问题是这样的，用input search做模糊搜索的时候，在键盘里面输入关键词，会通过ajax后台查询，然后返回数据，然后再对返回的数据进行关键词标红。用input监听键盘keyup事件，在安卓手机浏览器中是可以的，但是在ios手机浏览器中变红很慢，用输入法输入之后，并未立刻响应keyup事件，只有在通过删除之后才能相应！
- 解决办法:可以用html5的oninput事件去代替keyup,然后就达到类似keyup的效果！
```html
<input type="text" id="testInput">
<script type="text/javascript">
document.getElementById('testInput').addEventListener('input',function(e){
    var value = e.target.value;
});
</script>
```

## 9.部分机型存在type为search的input,自带close按钮样式修改方法;
- 有些机型的搜索input控件会自带close按钮(一个伪元素)，而通常为了兼容所有浏览器，我们会自己实现一个，此时去掉原生close按钮的方法为:
```css
#Search::-webkit-search-cancel-button{
    display:none;
}
```
- 如果想使用原生close按钮，又想使其符合设计风格，可以对这个伪元素的样式进行修改。

## 10.手机浏览器独有的四个事件
- onTouchmove,ontouchend,ontouchstart,ontouchcancel

## 11.为什么要用Zepto?
- jquery适用于PC端桌面环境，桌面环境更加复杂，jquery需要考虑的因素非常多，尤其表现在兼容性上面，相对于PC端，移动端的发展都远不及PC端,手机上的带宽永远比不上pc端。pc端下载jquery到本地只需要1~3秒（90+K），但是移动端就慢了很多，2G网络下你会看到一大片空白网页在加载，相信用户第二次就没打开的欲望了。zepto解决了这个问题，只有不到10K的大小，2G网络环境下也毫无压力，表现不逊色于jquery。

## IOS移动端click事件300ms的延迟响应
- 详解地址`https://gaodaxiu0406.github.io/2017/07/28/%E7%A7%BB%E5%8A%A8%E7%AB%AFclick300-380ms%E5%BB%B6%E8%BF%9F%E9%97%AE%E9%A2%98/`,这是之前做的关于这个问题的详细讲解地址

## 点击穿透问题,input、select、a等元素可以被点击和focus
- 这个在特定需求下才会有，因此如果没有类似问题的可以不看。首先需求是浮层操作，在手机上被遮罩的元素依然可以获取focus、click、change)，有两种解决方案：
    - 1.是通过层显示以后加入对应的class名控制，截断显示层下方可获取焦点元素的事件获取
    - 2.是通过将可获取焦点元素加入的disabled属性，也可以利用属性加dom锁定的方式（disabled的一种变换方式）


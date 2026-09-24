---
# 必填。项目名称。
title: "React轮播图（下）"
# 可选，和文章一样使用。
slug: react轮播图项目开写
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-07-31
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "react轮播图项目开写"
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

> 关于react轮播图的源码,无缝版已上传至[github,https://github.com/gaodaxiu0406/React-Slider](github,https://github.com/gaodaxiu0406/React-Slider)

<!-- more -->

## 用`react`+`webpack`写一个的轮播图项目(项目配置请看上篇[React轮播图（上）])

  先将整个文件写在一个文件中

## 1.画结构

- 新建一个components文件夹
- components文件夹下新建Slider.js文件和Slider.less文件(Slider.less文件是用来给Slider.js写样式的)

## 2.在indix.js中引入组件 渲染到页面中
- 打开src文件夹中的index.html文件
```html
<div id="root"></div>
```
- 2-1).在这个id为root的标签中渲染元素
- 2-2).回到index.js中,写一个轮播图组件，渲染到index.html中
```js
import React from 'react';
import ReactDOM from 'react-dom';
import Slider from './components/Slider';
let images=[
    {src:require('./images/1.jpg')},
    {src:require('./images/2.jpg')},
    {src:require('./images/3.jpg')},
    {src:require('./images/4.jpg')}
];
ReactDOM.render(<Slider images={images}/>,document.querySelector('#root'));
```
- 解释1)引入React，引入ReactDOM，引入Slider组件 然后通过ReactDOM.render将Slider组件渲染到index.html的id为root的div标签中
- 解释2)Slider组件需要图片参数
    - src文件夹下新建一个images文件夹，存入轮播的图片
    - 将图片路径通过require存入images数组中
    - 通过组件Slider标签将所需的images参数传入组件Slider(让images参数变量等于images数组)

## 3.开始写Slider.js中的代码
- 需要默认导出一个组件Slider供外面文件(index.js)调用;还需要接收一个images属性进行轮播
```js
import React from 'react';
import ReactDOM from 'react-dom';
require('./Slider.less');
export default class Slider extends React.Component{
    render(){
        let images=this.props.images;
        return(
            <div className="slider-wrapper">
                <ul className="sliders">
                    {       images.map((image,index)=>(
                    <li className="slider">
                    <img src={image.src}/>
                    </li>
                        ))
                    }
                </ul>
            </div>
        )
    }
}
```
- 1)`require('./Slider.less');`-->这里引入Slider.less用import和require都是一样的效果，都是加载一个模块的意思,模块可能是图片，可能是less/css/js/json文件,都可以-->在webpack中一切皆模块,不管是什么资源，都可以作为模块来加载
- 2)li的数量取决于images数据,images中有几张图片，就有几个li
    - 在render中let一个变量images来接收index.js传入的images,然后用map方法遍历整个数组
- 在Slider.less中写好轮播图的样式
```css
*{
  padding: 0;
  margin: 0;
}
ul,li{
  list-style: none;
}
.wrapper{
  width: 400px;
  height: 400px;
  position: relative;
  margin: 30px auto;
  .sliders{
    height: 400px;
    position: absolute;
    left:0;
    .slider{
      float: left;
      width: 400px;
      height: 400px;
      img{
        width: 100%;
        height: 100%;
      }
    }
  }
}
```
- 宽高为400px的轮播图

## 4.写配置文件
- 在webpack.config.js中加loaders
```css
module:{
        loaders:[
            {test:/\.js$/,loader:'babel-loader',exclude:/node_modules/},
            {test:/\.less$/,loader:'style-loader!css-loader!less-loader'},
            {test:/\.(jpg|png|gif)$/,loader:'url-loader'}
        ]
    }
```
- babel默认情况下什么都不做，需要一个配置文件.babelrc文件
    - 新建一个.babelrc配置文件
```css
{
  "presets": ["es2015","stage-0","react"]
}
```
- presets预设,"es2015"将es6编译成es5,"stage-0"将es7编译成es5,"react"将react编译成es5
- 原理1:`{test:/\.js$/,loader:'babel-loader',exclude:/node_modules/}`-->处理(编译)js文件:如果发现文件是js,用babel-loader加载,加载的时候需要读配置文件.babelrc,如果代码时es6/es7/react都要通过babel转成es5;同时通过exclude将node_modules文件夹下的所有js文件排除掉
- 原理2:`{test:/\.less$/,loader:'style-loader!css-loader!less-loader'}`-->如果发现文件以.less结尾的,第一步通过less-loader将less编译成css,然后通过css-loader进行加载,然后通过style-loader将他通过style标签的形式插入到页面中去，变成一个行内样式
- 原理3:`{test:/\.(jpg|png|gif)$/,loader:'url-loader'}`-->凡是资源文件都可以用url-loader来加载,不论是图片、图标、字体、视频、音频;后面可以通过问号传参,有个参数limit(例如:`{test:/\.(jpg|png|gif)$/,loader:'url-loader?limit=8192'}`-->小于8K的资源文件将直接以base64的形式内联在代码中，可以减少一次http请求)

### 此时执行`npm run build`,将代码打包到出口文件中,打开build文件夹下的index.html文件就可以直接预览效果了
- 此时会发现控制台有个报错
```js
Warning: Each child in an array or iterator should have a unique "key" prop. Check the render method of `Slider`. See https://fb.me/react-warning-keys for more information.
    in li (created by Slider)
    in Slider
```
- 需要唯一的key属性,在Slider.js文件中的li需要唯一的key属性，给li标签加上key属性即可
```html
<li className="slider" key={index}>                  <img src={image.src}/>        </li>
```
- 关掉浏览器,重新执行`npm run build`，再打开build文件夹下的index.html文件预览,控制台就没有报错了

## 5.写功能
- 让图片动起来,需要给Slider.js加个状态,需要有个定时器让他动起来 写在周期函数componentDidMount中
```js
constructor(){
        super();
        this.state={pos:0};//默认索引
    }
    componentDidMount(){
        this.$timer=setInterval(()=>{
            let pos=this.state.pos;
            pos++;//每隔2s让pos加1，pos值影响ul的左偏移量left的值 所以ul应该有个style属性 left值应该变化
            this.setState({pos:pos})

        },this.props.interval*1000)
```
- pos++;-->每隔2s让pos加1，pos值影响ul的左偏移量left的值 所以ul应该有个style属性 left值应该变化
    - ul应该有个style属性
    ```js
    render(){
            let images=this.props.images;
            let style={
                width:400*images.length,
                left:this.state.pos*-400
            };
            return(
                <div className="slider-wrapper">
                    <ul style={style} className="sliders">
                        {
                            images.map((image,index)=>(
                                <li className="slider" key={index}>
                                    <img src={image.src}/>
                                </li>
                            ))
                        }

                    </ul>
                </div>
            )
        }
    ```
- this.props.interval*1000-->每隔2s轮播一次,需要有变量传进来-->在index.js中新增一个interval变量(间隔时间让外面可以控制)
    - 1).这里通过this.props获取index.js中传递进来的的interval变量`this.props.interval*1000`
    - 2).index.js中新增一个interval变量
```js
ReactDOM.render(
    <Slider
        images={images}
        interval={2}
    />,document.querySelector('#root'));
```

### 写功能步骤总结:
- 第一步:定义一个默认索引pos,默认值是0
- 第二步:在组件加载完成之后创建定时器setInterval赋给this.$timer
- 第三步:每隔2s让图片向左偏移一个宽度的距离(interval是外界传进来的,是图片轮播的间隔时间),在index中要给组件Slider传进来一个2,2*1000意味着2s变一次
- this.$timer中先取出老的pos值，第一次轮播pos就是0，然后pos++，pos变成1，然后setState重新设置pos值,让pos值往上
- pos会影响ul的left值，一张图片的宽度是400px，向左偏移400，就是*-400
- ul的宽度应该是宽度400乘以图片的数量images.length,4张图就是1600px
### 执行`npm run dev`
- 注意,执行`npm run dev`可自动将文件编译更新打包到出口文件index.html中，并且只要更改文件，页面就会自动刷新,但是如果更改配置文件,需要重新启动`npm run dev`服务
- 此时执行`npm run dev`命令,轮播图就动起来了，但是越界了,因为此时还没有做边界处理

## 7.完善功能
- 将Slider需要的属性(可外界控制的)，在index.js的Slider组件标签中传入
```js
ReactDOM.render(
    <Slider
        images={images}//图片
        interval={2}//多长时间轮播一次
        speed={1}//每次轮播的速度
        pause={true}//当鼠标移动上去之后自动暂停
        autoplay={true}//是否启用自动轮播，false不自动轮播
                                  - 在Slider.js中
        dots={true}//是否有点状导航
        arrows={true}//是否有箭头导航
    />,document.querySelector('#root'));
```

- 添加`transitionDuration`-->规定完成过渡效果需要花费的时间 speed默认值是1 这里就是1s
```js
let style={
            width:400*images.length,
            left:this.state.pos*-400,
            transitionDuration:this.props.speed+'s'
        };
```

- 在Slider.js的周期函数中添加一个判断
```js
    componentDidMount(){
        if(this.props.autoPlay){
            this.$timer=setInterval(()=>{
                let pos=this.state.pos;
                pos++;
                this.setState({pos:pos})
            },this.props.interval*1000)
        }
    }
```
- this.props.autoPlay 是否自动轮播 如果外界传入true就是自动轮播，传入false就是不自动轮播

## 8.将轮播切换单独拎出来写成一个方法turn
```js
    turn(n){
        let pos=this.state.pos;
        pos+=n;
        this.setState({pos:pos})
    }
```
- 或者使用es6的箭头函数
```js
turn=(n)=>{
        let pos=this.state.pos;
        pos+=n;
        this.setState({pos:pos})
    }
```
- `let pos=this.state.pos;`获取旧索引
- turn表示切换,n表示切换的步长,方便以后操作:例如往左走传1进来即可，往右走传-1进来即可
- 那么此时在周期函数中,直接调用这个turn方法即可,默认往右轮播，传入-1
```js
    componentDidMount(){
        if(this.props.autoplay){
            this.timer=setInterval(()=>{
                this.turn(1);
            },this.props.interval*1000)
        }
    }
```
## 9.实现鼠标移上去停止轮播
- 给div加onMouseOver和onMouseOut事件
```js
<ul onMouseOver={()=>clearInterval(this.timer)} onMouseOut={this.play} style={style} className="sliders">
...
</ul>
```
## 10.自动轮播部分也封装成一个函数play
```js
play=()=>{
        this.timer=setInterval(()=>{
            this.turn(1);
        },this.props.interval*1000)
    };
```
- play表示开启定时器进行自动轮播
- 那么此时在周期函数中直接调用`this.play()`即可
```js
    componentDidMount(){
        if(this.props.autoplay){
            this.play();
        }
    }
```
## 11.边界判断
```js
turn=(n)=>{
        let pos=this.state.pos;
        pos+=n;
        if(pos>=this.props.images.length){
            pos=0;
        }
        this.setState({pos:pos})
    };
```
- 当索引为图片总张数的时候 让索引变为0
## 12.写左右箭头
- 在ul下加一个div
```html
<div className="arrows">
                    <span className="arrow-left">&lt;</span>
                    <span className="arrow-right">&gt;</span>
                </div>
```
- 在Slider.less中写样式
```css
  .arrows{
    position: absolute;
    width: 100%;
    height: 20px;
    top:50%;
    margin-top:-10px;
    .arrow{
      width: 20px;
      height: 20px;
      line-height: 20px;
      text-align: center;
      cursor: pointer;
      font-size: 30px;
      background-color: #eee;
      &:hover{
        background-color: #999;
      }
    }
    .arrow-left{
      margin-left: 5px;
      float: left;
    }
    .arrow-right{
      margin-right: 5px;
      float: right;
    }
  }
```
- 给左右arrow绑定事件
```html
                <div className="arrows">
                    <span onClick={()=>this.turn(-1)} className="arrow arrow-left">&lt;</span>
                    <span onClick={()=>this.turn(1)} className="arrow arrow-right">&gt;</span>
                </div>
```
## 13.处理左边界
- 在turn中做个判断
```js
    turn=(n)=>{
        let pos=this.state.pos;
        pos+=n;
        if(pos>=this.props.images.length){
            pos=0;
        }
        if(pos<0){
            pos=this.props.images.length-1;
        }
        this.setState({pos:pos})
    };
```
- 当索引小于0的时候,让索引等于images的长度-1

## 14.根据传进来的arrows值判断是否有左右箭头切换效果
- 第一种方法(看着比较乱)
```js
{
    this.props.arrows?<div className="arrows">
        <span onClick={()=>this.turn(-1)} className="arrow arrow-left">&lt;</span>
        <span onClick={()=>this.turn(1)} className="arrow arrow-right">&gt;</span>
    </div>:null
}
```
- 第二种,在render中
```js
let arrows=null;
        if(this.props.arrows){
            arrows=(
                <div className="arrows">
                    <span onClick={()=>this.turn(-1)} className="arrow arrow-left">&lt;</span>
                    <span onClick={()=>this.turn(1)} className="arrow arrow-right">&gt;</span>
                </div>
            )
        }
```
- 那么ul下面就可以直接用{arrows}代替了(看着很清晰明了)
```html
<div className="slider-wrapper">
    <ul onMouseOver={()=>clearInterval(this.timer)} onMouseOut={this.play} style={style} className="sliders">
        {
            images.map((image,index)=>(
                <li className="slider" key={index}>
                    <img src={image.src}/>
                </li>
            ))
        }
    </ul>
{arrows}
</div>
```

## 15.根据传进来的dots值判断是否有点状导航
```js
let dots=null;
    if(this.props.dots){
        dots=(
            <div className="dots">
                {
                    images.map((image,index)=>(
                        <span className="dot" key={index}></span>
                    ))
                }
            </div>
        )
    }
```
- dots直接放到最下面即可
```
...
{arrows}
{dots}
```
### 15-1.在Slider.less中写dots的样式
```css
  .dots{
    width: 100%;
    height: 20px;
    position: absolute;
    bottom: 10px;
    text-align: center;
    .dot{
      display: inline-block;
      width: 20px;
      height: 20px;
      border-radius: 50%;
      margin-left: 5px;
      background-color: #abcdef;
      cursor: pointer;
      &:hover{
        background-color: #999999;
      }
    }
  }
```
## 16.点状导航的点击跟随事件
- 给span加onClick事件
```html
···
<span className="dot" key={index} onClick={()=>this.turn(index-this.props.pos)}></span>
···
```
### 16-1.轮播点状导航自动跟随事件
- 在Slider.less中加一个active样式
```css
.active{
    background-color: #999999;
  }
```
- 给span标签添加active属性
```html
<span className={"dot "+(index==this.state.pos?'active':'')} key={index} onClick={()=>this.turn(index-this.state.pos)}></span>
```

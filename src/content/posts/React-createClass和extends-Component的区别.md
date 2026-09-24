---
# 必填。项目名称。
title: "React.createClass和extends Component的区别(转载)"
# 可选，和文章一样使用。
slug: React.createClass和extends Component的区别(转载)
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-09-09
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "React.createClass和extends Component的区别(转载)"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/webstore打开设置窗口.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: React
tags:
  - react
  - react.createClass
  - extends Component
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

> `createClass`本质上是一个工厂函数，`extends`的方式更加接近最新的ES6规范的`class`写法。两种方式在语法上的差别主要体现在方法的定义和静态属性的声明上。`createClass`方式的方法定义使用逗号`,`隔开，因为`creatClass`本质上是一个函数，传递给它的是一个`Object`；而`class`的方式定义方法时务必谨记不要使用逗号隔开，这是`ES6 class`的语法规范。

<!-- more -->
### `React.createClass`和`extends Component`的区别主要在于：

- 语法区别
- propType 和 getDefaultProps
- 状态的区别
- this区别
- Mixins

## 1.语法区别

- React.createClass

```js
import React from 'react';
const Contacts = React.createClass({
  render() {
    return (
      <div></div>
    );
  }
});
export default Contacts;
```

- React.Component

```js
import React from 'react';

class Contacts extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div></div>
    );
  }
}

export default Contacts;
```

- 后一种方法使用ES6的语法，用constructor构造器来构造默认的属性和状态。

## 2.`propType`和`getDefaultProps`

- `React.createClass`: 通过`proTypes`对象和`getDefaultProps()`方法来设置和获取`props`

```js
import React from 'react';

const Contacts = React.createClass({
  propTypes: {
    name: React.PropTypes.string
  },
  getDefaultProps() {
    return {

    };
  },
  render() {
    return (
      <div></div>
    );
  }
});

export default Contacts;
```

- `React.Component`：通过设置两个属性`propTypes`和`defaultProps`

```js
import React form 'react';
class TodoItem extends React.Component{
    static propTypes = { // as static property
        name: React.PropTypes.string
    };
    static defaultProps = { // as static property
        name: ''
    };
    constructor(props){
        super(props)
    }
    render(){
        return <div></div>
    }
}
```

## 3.状态的区别

- `React.createClass`：通过`getInitialState()`方法返回一个包含初始值的对象

```js
import React from 'react';
   let TodoItem = React.createClass({
       // return an object
       getInitialState(){
           return {
               isEditing: false
           }
       }
       render(){
           return <div></div>
       }
   })
```

- `React.Component`：通过`constructor`设置初始状态

```js
import React from 'react';
  class TodoItem extends React.Component{
      constructor(props){
          super(props);
          this.state = { // define this.state in constructor
              isEditing: false
          }
      }
      render(){
          return <div></div>
      }
  }
```

## 4.this区别

- `React.createClass`：会正确绑定`this`

```js
import React from 'react';

const Contacts = React.createClass({
  handleClick() {
    console.log(this); // React Component instance
  },
  render() {
    return (
      <div onClick={this.handleClick}></div>//会切换到正确的this上下文
    );
  }
});

export default Contacts;
```

- `React.Component`：由于使用了 `ES6`，这里会有些微不同，属性并不会自动绑定到 `React` 类的实例上。

```js
import React from 'react';
class TodoItem extends React.Component{
  constructor(props){
    super(props);
  }
  handleClick(){
    console.log(this); // null
  }
  handleFocus(){  // manually bind this
    console.log(this); // React Component Instance
  }
  handleBlur: ()=>{  // use arrow function
    console.log(this); // React Component Instance
  }
  render(){
    return <input onClick={this.handleClick}
      onFocus={this.handleFocus.bind(this)}
      onBlur={this.handleBlur}/>
  }
}
```

- 我们还可以在 `constructor` 中来改变 `this.handleClick` 执行的上下文，这应该是相对上面一种来说更好的办法，万一我们需要改变语法结构，这种方式完全不需要去改动 `JSX` 的部分：

```js
import React from 'react';

class Contacts extends React.Component {
  constructor(props) {
    super(props);
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    console.log(this); // React Component instance
  }
  render() {
    return (
      <div onClick={this.handleClick}></div>
    );
  }
}

export default Contacts;
```

## 5.`Mixins`

- 如果我们使用 `ES6` 的方式来创建组件，那么 `React mixins` 的特性将不能被使用了。

```js
React.createClass：使用 React.createClass 的话，我们可以在创建组件时添加一个叫做 mixins 的属性，并将可供混合的类的集合以数组的形式赋给 mixins。

import React from 'react';
let MyMixin = {
    doSomething(){}
}
let TodoItem = React.createClass({
    mixins: [MyMixin], // add mixin
    render(){
        return <div></div>
    }
})
```

> 原文链接[https://segmentfault.com/a/1190000005863630](https://segmentfault.com/a/1190000005863630)

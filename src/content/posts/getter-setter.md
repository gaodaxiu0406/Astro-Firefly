---
# 必填。项目名称。
title: "getter&setter"
# 可选，和文章一样使用。
slug: getter&setter
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-09-05
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "getter&setter"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Javascript
tags:
  - JS
  - Javascript
  - getter
  - setter
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

### 一般在书上看到都解释都是 把成员变量直接暴露在外不符合OOP的封装性原则，不安全，应该使用getter和setter方法来取值和赋值。但是没有解释为什么不符合OOP的封装性原则，为什么不安全，一个成员变量不就是取值和赋值这么两个操作吗，还能干什么，暴露出来又怎么样？

<!-- more -->
- 的确可以暴露，如果
  - 1. 所有内外代码都是你自己写；
  - 2. 这个模块再也不改了；
  - 3. 不会继承它，或者继承但不改变语义。
- David John Wheeler有一句名言：“All problems in computer science can be solved by another level of indirection(翻译:“计算机科学中的所有问题都可以通过另一种间接方式来解决).”getter、setter就是个很好的中间层。
- 直接摘录stackoverflow上一个不错的总结：
- oop - Why use getters and setters?
  - 1.这两个方法可以方便增加额外功能（比如验证）。
  - 2.内部存储和外部表现不同。
  - 3.可以保持外部接口不变的情况下，修改内部存储方式和逻辑。
  - 4.任意管理变量的生命周期和内存存储方式。提供一个debug接口。
  - 5.能够和模拟对象、序列化乃至WPF库等融合。
  - 6.允许继承者改变语义。
  - 7.可以将getter、setter用于lambda表达式。（大概即作为一个函数，参与函数传递和运算）
  - 8.getter和setter可以有不同的访问级别。
- lambda表达式
- Lambda 表达式”(lambda expression)是一个匿名函数，Lambda表达式基于数学中的λ演算得名，直接对应于其中的lambda抽象(lambda abstraction)，是一个匿名函数，即没有函数名的函数。Lambda表达式可以表示闭包（注意和数学传统意义上的不同）。
  - lambda  ` ['læmdə]`  希腊字母的第11个λ
  - expression  `[ɪkˈspreʃn]`  表达
  - abstraction  `[əb'strækʃ(ə)n]`  抽象概念

### 以下为转载

> Compiling the list up here at the top of what seemed winners to me, from the viewpoint of a Java web dev:(从Java web开发人员的角度来看，在我看来是赢家的列表上面列出了这个列表:)

- 1.When you realize you need to do more than just set and get the value, you don't have to change every file in the codebase.当您意识到您需要做的不仅仅是设置和获取值时，您不必更改代码库中的每个文件。
- 2.You can perform validation here.您可以在这里执行验证。
- 3.You can change the value being set.您可以更改设置的值。
- 4.You can hide the internal representation. getAddress() could actually be getting several fields for you.您可以隐藏内部表示。getAddress()实际上可以为您获取多个字段。
- 5.You've insulated your public interface from changes under the sheets.您已经将您的公共接口与表单下的更改隔离了。
- 6.Some libraries expect this. Reflection, serialization, mock objects.一些图书馆预计。反射,序列化,模拟对象。
- 7.Inheriting this class, you can override default functionality.继承这个类，您可以覆盖默认的功能。
- 8.You can have different access levels for getter and setter.对于getter和setter，您可以有不同的访问级别。
- 9.Lazy loading.延迟加载；懒装载；懒加载
- 10.People can easily tell you didn't use Python.人们可以很容易地告诉您，您没有使用Python。

#### 参考链接:
- [https://stackoverflow.com/questions/1568091/why-use-getters-and-setters](https://stackoverflow.com/questions/1568091/why-use-getters-and-setters)
- [https://www.zhihu.com/question/21401198/answer/18113707](https://www.zhihu.com/question/21401198/answer/18113707)

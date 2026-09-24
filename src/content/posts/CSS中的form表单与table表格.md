---
# 必填。项目名称。
title: "CSS中的form表单与table表格"
# 可选，和文章一样使用。
slug: CSS中的form表单与table表格
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2017-06-30
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "CSS中的form表单与table表格"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: CSS
tags:
  - CSS
  - form
  - table
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---
### form表单
- 用来获取用户信息`<form></form>`
<!-- more -->
```html
<form>
    <input type="radio" name="ok" checked="checked"><!--单选按钮--><label>满意</label><!--label 描述表单元素功能-->
    <!--type 类型-->
    <!--name 名字-->
    <!--checked 选中-->
    <input type="radio" name="ok"><!--单选按钮--><label>不满意</label>
    <input type="checkbox"><label>篮球</label>
    <input type="checkbox" checked><label>美女</label>
    <input type="checkbox"><label>彭于晏</label>
    <input type="checkbox"><label>陈冠希</label>
    <input type="checkbox"><label>杨颖</label>
    <input type="checkbox"><label>维密</label>

    <textarea maxlength="10" minlength="1"></textarea><!--文本域-->
    <!--maxlength 字符输入的最大长度-->
    <br>
    <label>姓名</label><input type="text">
    <br>
    <label>手机</label><input type="text">
    <br>
    <label>密码</label><input type="password">
</form>
```

- radio 单选按钮
    -  name="ok"（name的值相同情况下）同时给到input type="radio"，表示单选只能选中其中的一个
- lable描述表单元素功能
- type 类型
- name 名字
- cheked 选中
    - 单独写checked也可以达到选中的效果
- `<input type="checkbox">`checkbox 多选按钮
- textarea 文本域
- `<textarea maxlength="10" minlength="1"></textarea>`
    - maxlength字符输入的最大长度

### table表格
- `<caption>标题</caption>`
- `<thead>表头</thead>`
    - tr>th（标题单元格，th加粗居中）
- `<tfoot>` 表尾
    - tr>th（普通单元格）
    - tr>td（普通单元格，td不加粗不居中）
- tbody 表身
    - tr>th（普通单元格）
> thead和tfoot分别有一个 tbody可以有多个
> tfoot一般放置在thead的后面，为了防止tbody中的内容过多，tfoot加载过慢的情况，但是虽然书写位置在前面，在页面中显示的时候，这部分依然在整个表格的最后面
> 如果table用来搭建结构，我们只需写tr和td
```html
<table>
    <tr>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
         <td></td>
         <td></td>
         <td></td>
    </tr>
</table>
```
---
title: CSS 4

language_tabs:
  - Demo

search: true
---

# 概述a

该文档主要介绍了CSS 4的一些新特性，包括Selectors level 4, Filter effects level 1。
其他新特性及模块暂时未总结。


# Selectors Level 4

CSS选择器第四版

## 逻辑组合 Logical Combinations

### :matches(s1, s2, …)

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/zo6ma105/1/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

匹配任一选择器，可将多个选择器合并。

`li a:link, li a:hover, li a:visited, li a:focus`

`=> li a:matches(:link, :hover, :visited, :focus)`

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
12+ (-webkit-) | 5+ (-webkit-) | 4+ (-moz-) | 15+ (-webkit-) | No | ? | 5+ (-webkit-)

<aside class="notice">
只有最新的Safari同时支持:matches和:any, 其他浏览器目前只支持:any
</aside>

### :not(s1, s2, …)

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/4sLjg7ve/1/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

CSS 3中已有该选择器，但参数只允许一个选择器；在CSS 4中允许多个选择器作为参数。

`li:not(.nobg, :first-child)`

选取除了第一个元素和class为noby的li元素


&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | latest | No | No | No | No | No


### :has(s1, s2, …)

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/k8h9qyru/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>



`li:has(> span)`

选取子元素为span的li元素


&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | No | No | No | No | No


## 属性选择器 Attribute selectors

### Case-sensitivity

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/k8h9qyru/1/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

属性选择器中包含`i`标识符，无论在大小写敏感的文档语言（eg.XML）或不敏感的文档语言（eg.HTML）中，都将忽略属性名和属性值的大小写。

`[attr="VAL" i]`


&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
49.0 | 9 | 47.0 | ? | ? | ? | 9


## 语言伪类 Linguistic Pseudo-classes

### :lang

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/k8h9qyru/2/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

CSS 2中已有该选择器，在CSS 4中新增了通配符`*`。

`span:lang(*-CA)`

选取所有lang属性以’-CA’结尾（en-CA, fr-CA）的span标签


&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | No | No | No | No | No


### :dir(ltr or rtl)

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/xrym2Lhy/1/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

用于匹配文字方向的伪类选择器，选择器参数可为`ltr`（从左到右） 或 `rtl`（从右到左）。


`p:dir(rtl)`

选取文字方向为从右到左的p标签


&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | 17+ (-moz-) | No | No | No | No



## 链接伪类 Location Pseudo-classes

### :any-link

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/zo6ma105/2/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

该伪类选择器适用于拥有`href`属性的元素。

`a:any-link`

a标签（所有状态，eg.:hover, :visited, …）都将被选中


&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | latest | No | No | No | No | No

<aside class="warning">
名字很可能被换掉，W3C正在征求新的名字
</aside>

### :scope

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/ep10ozcn/embedded/html,css,result/dark/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

匹配标记为scoped的style元素的父级元素。


&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | 21+ | No | No | No | No

<aside class="warning">
该选择器在Chrome 35版本中被移除
</aside>

## 用户行为伪类 User Action Pseudo-classes

### :focus-within

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/ob91skow/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

当某个元素的:focus被应用，这个元素及祖先元素的:focus-within也会被匹配。


&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | No | No | No | No | No


### :drop

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/gyqmgeyw/1/embedded/js,html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

应用于“放”的目标元素。

`:drop(active || valid || invalid):`

* **active:** 当`drop target`是当前元素时
* **valid:** 当`drop target`有`valid`和`invalid`状态之分时（比如`dropzone`属性中可以指定拖拽元素的类型）, 匹配`valid`的`drop target`；否则，匹配所有`drop target`。
* **invalid:** 当`drop target`有`valid`和`invalid`状态之分时（比如`dropzone`属性中可以指定拖拽元素的类型）, 匹配`valid`的`drop target`；否则，不匹配任何元素。

`:drop() => :drop`

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | No | No | No | No | No

<aside class="notice">
`dropzone`属性还在working draft状态中，各个浏览器暂时没发现支持的...
</aside>

## 状态伪类 Time-dimensional Pseudo-classes

### :current(s1, s2, …)

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/dz5ezvtn/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

时间维度的元素（eg.视频字幕，读屏）处于’当前状态’时应用此伪类。


&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | No | No | No | No | No

### :past(s1, s2, …)

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/dz5ezvtn/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

时间维度的元素（eg.视频字幕，读屏）处于’当前状态’之前时应用此伪类。


&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | No | No | No | No | No

### :future(s1, s2, …)

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/dz5ezvtn/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

时间维度的元素（eg.视频字幕，读屏）处于’当前状态’之后时应用此伪类。


&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | No | No | No | No | No

## 表单伪类 The Input Pseudo-classes
### :read-only & :read-write

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/pzuxefy6/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

* **`:read-only`** 匹配内容不可编辑的元素
* **`:read-write`** 匹配内容可编辑的元素（input或contenteditable为true的元素）

| | Chrome | Safari | Firefox | Opera | IE | Android | ios
| --------- | --------- | ------- | ------- | ------- | ------- | ------- | -------
| 基础支持 | Yes | Yes | -moz- | ? | ? | ? | Yes
| contenteditable | latest | latest | -moz- | ? | ? | ? | ?


### :placeholder-shown

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/ybzkbkyo/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

各个浏览器已实现相应等价的选择器，命名使用的是`-vendor-input-placeholder`。

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
-webkit- | -webkit- | 4~18 (:-moz-) 19+ (::-moz-) | 15+ (-webkit-) | 10+ (:-ms-) Edge(::-ms-) | -webkit- | 4+ (-webkit-)

### :default

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/zatykbwn/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

匹配默认元素（eg.select的第一个option, form表单默认的submit button等）。

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
10.0 | 5.0 | 4.0 | 10.0 | No | ？ | 5.0

### :indeterminate

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/23oaaz1n/embedded/js,html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

当一个元素的值处于不确定状态时匹配，比如checkbox有checked、unchecked和indeterminate三种状态。

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
Yes | 3.0 | 3.6 | 10.60 | 9.0 | ？ | ?

<aside class="notice">
Chrome中`type="radio"`的元素也支持该伪类。
</aside>

### :valid & :invalid

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/8gh1sbjf/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

匹配元素(form, input)验证通过或不通过的状态，有些元素没有验证机制（eg.p标签）则不会被匹配。

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
10.0 | 5.0 | 4.0 | 10.0 | 10(只支持input) | ？ | 5.0

### :in-range & :out-of-range

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/pgzzen75/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

匹配元素的值在范围内或范围外，无范围限制的元素或者非表单元素都不会被匹配到。

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
10.0 | 5.2 | 29.0 | 11.0 | No | 2.3 | Yes

### :required & :optional

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/8gh1sbjf/1/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

:required匹配有required属性的input元素，:optional则相反。

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
10.0 | 5.0 | 4.0 | 10.0 | 10 | ？ | 5.0

### :user-invalid

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/zxnay2Ld/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

form表单出错并不会匹配该伪类，只有当用户显著触发（比如提交表单）才会被匹配。

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | No | No | No | No | No

## 结构伪类 Tree-Structural

### :blank

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/hywgLhwq/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

和:empty相似，但:blank可以匹配到仅包含空格、tab、换行符的元素。

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | -moz- | No | No | No | No

<aside class="notice">
Firefox中:-moz-only-whitespace与:blank等价
</aside>

<aside class="warning">
W3C在征集新的名字以取代`blank`
</aside>


### :nth-child(An+B [of S])

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/405c7t6t/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

:nth-child, :nth-of-type均为css3的选择器，css4中新加了对:nth-child选择器的过滤。

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | latest | No | No | No | No | ?

<aside class="notice">
span:nth-of-type(2) => :nth-child(2 of span)
</aside>

## 后代选择器 Descendant combinator

### 后代选择器>>

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/vzzq8pmk/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

CSS3中后代选择器是通过`空格`表示的（eg.div span），CSS4中新增了`>>`符号来表示，与`空格`等价。

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | No | No | No | No | No

<aside class="notice">
div span => div >> span
</aside>

## 网格选择器 Grid-Structural Selectors

### 列关系选择器||&nbsp;

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/t9s4L03a/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

`col || cell`

该选择器表明`单元格`和`列`的关系。

`col.selected || td`  选取class为selected列下的td元素; 在此选择器之前，可以使用:nth-child来选取单元，当设置`colspan`属性时，选取的列不一定是正确的（看demo）

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | No | No | No | No | No

### :nth-column(An+B)

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/t9s4L03a/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

`n为整数`

选取符合An+B的列，从第一列开始匹配。

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | No | No | No | No | No


### :nth-last-column(An+B)

<iframe style="float:right;" width="50%" height="300" src="//jsfiddle.net/adayan/t9s4L03a/embedded/html,css,result/dark" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

`n为整数`

选取符合An+B的列，从最后一列开始匹配。

&nbsp;

Chrome | Safari | Firefox | Opera | IE | Android | ios
--------- | ------- | ------- | ------- | ------- | ------- | -------
No | No | No | No | No | No | No



---
title: 浅谈 CSS 选择器优先级的计算规则
tags: 
	- CSS
	- WEB 标准
categories:
	- CSS
date: 2022-05-31 19:39:00
hidden: false
---

CSS优先级是一个值得思考的问题，再次之前我对CSS优先级的理解是:

> !important>内联样式>ID选择器>类选择器>类型选择器

相信很多人对CSS优先级的理解也是这样的，但是一篇文章([CSS选择器的优先级（精讲版） (biancheng.net)](http://c.biancheng.net/view/7216.html))上面书写了关于**CSS 选择器优先级的计算规则**的内容，使我开始对CSS优先级进行重新研究。

根据W3C给出关于选择器特异性(specificity，国内一般称优先级)的解释，选择器分为ABC三个等级，其中A为ID选择器，B包括类选择器、属性选择器和伪类，C包括类型选择器和伪元素，当然还存在一个通用选择器，但是通用选择器一般忽略。

| 等级 | 包含选择器                                   |
| ---- | -------------------------------------------- |
| A    | 计算选择器中 ID 选择器的数量                 |
| B    | 计算选择器中类选择器、属性选择器和伪类的数量 |
| C    | 计算选择器中类型选择器和伪元素的数量         |

优先级的计算，从A级开始到C级结束，如果到C级是两个选择器的优先级还是相等的那么有限选择靠后的选择器。

### 重复简单选择器

CSS选择器允许重复出现简单选择器，并且简单选择器的重复出现会增加优先级。

```css
.class.class{
    background-color: red;
}

.class{
    background-color: green;
}
```

也就是说如上代码中第一个选择器重复出现了`.class`选择器，第二个选择器只出现了一个`.class`选择器，这两种写法都是正确的，并且第一个选择器`.class.class`的优先级大于第二个选择器`.class`，所以结果是背景颜色将呈现红色。

| 选择器       | 优先级 (A, B, C) |
| ------------ | ---------------- |
| .class.class | (0, 2, 0)        |
| .class       | (0, 1, 0)        |

> 在低版本CSS中可能简单重复选择器会被忽略，如在ie8中重复id或被忽略，在ie5中重复的class或被忽略。
>
> 拒绝IE，从我做起！

### 特殊选择器

一些伪类和其他选择器中存在一些特殊的选择器，因此单独定义了这些特殊选择器的特异性。

1. 选择器`:is()`、`:not()`、`:has()`的优先级是选择器列表中最具有复杂性的选择器的优先级取代。
2. 选择器`:nth-child()`、`:nth-last-child()`的优先级是伪类本身的优先级（计为一个伪类选择器，也就是计为B），再加上选择器列表中最具复杂性的选择器的优先级。
3. 选择器`:where()`伪类的优先级被零代替，也就是没有优先级，再优先级计算中不做数。
4. 通用选择符以及其他选择符在优先级中不计数。

### 优先级计算

| 选择器                                              | 优先级 (A, B, C) |
| -------------------------------------------------- | ---------------- |
| .class                                             | (0, 1, 0)        |
| #Red                                               | (1, 0, 0)        |
| .container :is(.container>#Red, .container>.class) | (1, 2, 0)        |
| .container #Red.class:nth-child(1)                 | (1, 3, 0)        |
| :is(.container>.class.class)                       | (0, 3, 0)        |
| #Red:is(.container>.class)                         | (1, 2, 0)        |
| .container div:nth-child(1)                        | (0, 2, 1)        |
| :is(#Red.class)                                    | (1, 1, 0)        |
| #Red.class                                         | (1, 1, 0)        |
| #Red.class:nth-child(1)                            | (1, 2, 0)        |
| #Red#Red                                           | (2, 0, 0)        |

[代码片段](https://code.juejin.cn/pen/7103862825264611359)

[codepen](https://codepen.io/onemue/pen/RwQMBmd)

### specificity求和

在一些其他文档中将讲A、B、C分别比作100,10,1 进行求和，是不准确的，如果按照这样做那么10个class是不是相当于一个id，显然不是。

在[CSS Level 1](https://www.w3.org/TR/CSS1/#cascading-order)、[Selectors Level 3](https://drafts.csswg.org/selectors-3/#specificity)中也有这样的描述。

在主流浏览器中高等级高于低等级是即使ABC求和相同也不会优先使用后声明的CSS。

造成这样的原因是**权重的进制是并不是十进制，CSS 权重进制在 IE6 为 256，后来扩大到了 65536，现代浏览器则采用更大的数量**。也可以理解**选择器的权值不能进位**，或者理解为选择器权值ABC单独计算比较。

### 关于`!important `

MDN指出“使用 `!important` 是一个**坏习惯**，应该尽量避免”，并给出了使用`!important` 的情况：

- **一定**要优先考虑使用样式规则的优先级来解决问题而不是 `!important`
- **只有**在需要覆盖全站或外部 CSS 的特定页面中使用 `!important`
- **永远不要**在你的插件中使用 `!important`
- **永远不要**在全站范围的 CSS 代码中使用 `!important`

以及替代 `!important`的方法:

1. 更好地利用 CSS 级联属性
2. 使用更具体的规则。在您选择的元素之前，增加一个或多个其他元素，使选择器变得更加具体，并获得更高的优先级。
3. 对于（2）的一种特殊情况，当您无其他要指定的内容时，请复制简单的选择器以增加特异性。

推荐阅读[优先级 - CSS（层叠样式表） | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Specificity#!important_例外规则)，了解更多`!important`的使用意见。
### 其他 CSS 优先规则

**CSS 优先规则1：** 最近的祖先样式比其他祖先样式优先级高。

**CSS 优先规则2：** "直接样式"比"祖先样式"优先级高。

**CSS 优先规则3：** 优先级关系：内联样式 > ID 选择器 > 类选择器 = 属性选择器 = 伪类选择器 > 标签选择器 = 伪元素选择器。

**CSS 优先规则4：** 计算选择符中 ID 选择器的个数（a），计算选择符中类选择器、属性选择器以及伪类选择器的个数之和（b），计算选择符中标签选择器和伪元素选择器的个数之和（c）。按 a、b、c 的顺序依次比较大小，大的则优先级高，相等则比较下一个。若最后两个的选择符中 a、b、c 都相等，则按照"就近原则"来判断。

**CSS 优先规则5：** 属性后插有 **!important** 的属性拥有最高优先级。若同时插有 **!important**，则再利用规则 3、4 判断优先级。

> 注意: 文档树中元素的接近度（[Proximity of elements](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Specificity#无视DOM树中的距离)）对优先级没有影响。

### 参考文献

1. [Selectors Level 4](http://www.w3.org/TR/selectors/#specificity)
2. [优先级 - CSS（层叠样式表） | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Specificity)
3. [CSS 样式优先级 | 菜鸟教程 (runoob.com)](https://www.runoob.com/w3cnote/css-style-priority.html)
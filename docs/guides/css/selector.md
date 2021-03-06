---
title: 请说说`css`的选择器以及选择器优先级
---

# 请说说`css`的选择器以及选择器优先级

## 前言

选择器的基本规则大致是是以下的方式，基本的作用就是选择 `html` 元素
```
选择器{
  属性 值;
  属性 值
}
```
需要注意的是，浏览器去找元素的时候，是`从右往左` 的方式

```css
div .box a {

}
```

`!important > 内联样式 = 外联样式 > ID选择器 > 类选择器 = 伪类选择器 = 属性选择器 > 元素选择器 = 伪元素选择器 > 通配选择器 = 后代选择器 = 兄弟选择器`

这里会牵扯一个权重的问题 直观来看

```
 10000：!important
 1000：内联样式、外联样式
 100：ID选择器
 10：类选择器、伪类选择器、属性选择器
 1：元素选择器、伪元素选择器
 0：通配选择器、后代选择器、兄弟选择器
```

## 选择器

### 选择器的基本分类

 - 类选择器
 - ID 选择器 页面中一般是唯一的
 - 元素选择器
 - 伪元素选择器(连续有；两个英文冒号) ::before 不会dom树中
 - 属性选择器 [type=radio]{}
 - 伪类选择器 :hover :first-child :last-child
 - 组合选择器
 - 否定的选择器 反向选择
 - 通用选择器

> 基本的选择器

| 选择器 | 别名       | 使用 |
| ------ | ---------- | ---- |
| \*     | 通配符     | \*{} |
| tag    | 标签选择器 | p{}  |
| .class | 类         | .{}  |
| #id    | id 选择器  | #{}  |

> 关系选择器
常见的符号 > ~ +

 - 后代选择器
 - 相邻后代 > 仅仅选择合乎规则的的兄弟元素
 - 兄弟选择器 ~ 选择当前元素后面的合乎规则的元素
 - 相邻兄弟 + 选择当前元素相邻的合乎规则的的兄弟元素



## 选择器的权重
优先级高的层叠优先级较低 的样式，其实是比较复杂的问题

|     选择器     |  权重位  |
| :------------: | :------: |
|      行内      |  +1000   |
|       id       |  +0100   |
| 类选择器、属性 |  +0010   |
|  元素、伪元素  |  + 0001  |
|       \*       |  +0000   |
|      继承      | 没有权重 |

通过 `color: powderblue !important;` 提高自己的权重（其优先级是最高的），那相同的权重后写的生效

---
title: css单位有哪些以及它们的区别
---

# css单位有哪些以及它们的区别



>分辨率1920×1080意味着水平方向含有1920个像素数，垂直方向含有1080个像素数
> 超小的屏幕（移动设备） 768px 以下
> 小屏设备 768px-992px
> 中屏设备 992px-1200px
> 宽屏设备 1200px 以上

在我们写样式修饰的时候，`长度单位`像PX、EM、REM是我们常用的。那么它们有什么不同的地方呢？
我们这里重点说下长度单位：分为相对长度单位和绝对长度单位

 - 相对长度
   - 相对字体：em rem(css3)
   - 相对视区 vh vw vmin vmax

 - 绝对长度 px 其他的基本不用就不提了 
### 1、PX 

像素。Pixel，相对于显示器的屏幕分辨率的大小

- IE无法调整那些使用px作为单位的字体大小
- 国外大部分的网站能够调整的原因在于其使用了em或者rem作为字体大小

### 2、em

em相对长度单位`相对于当前对象内文本的字体尺寸`

- 参考物是父元素的font-size
- 当前父元素没有设置字体尺寸 ，相对于浏览器的默认字体大小
- em的值不是固定的
- em会继承父级元素的字体大小

### 3、rem

rem是css3新增的一个相对单位，rem是相对于HTML根元素的字体大小的长度单位

- 优点 只需要设置根目录的大小就可以把整个页面的的比例调好
- 兼容性 ie8 更早的版本

### 4、vw、vh

vw、vh、vmax、vmin 这四个单位基于视口

vw是相对视口的宽度而定的 长度等于视口宽度的1/100

vh是相对视口（viewport）的高度而定的，长度等于视口高度的1/100

### 5、%（百分比）

一般来说就是相对于父元素

1、对于普通定位元素就是我们理解的父元素

2、对于position: absolute;的元素是相对于已定位的父元素

3、对于position: fixed;的元素是相对于ViewPort（可视窗口）



### 6、vm

css3新单位，相对于视口的宽度或高度中较小的那个

其中最小的那个被均分为100单位的vm

比如：浏览器高度900px，宽度1200px，取最小的浏览器高度，1 vm = 900px/100 = 9 px

缺点：兼容性差

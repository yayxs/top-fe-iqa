[TOC]

## 前言

这次分享的前端相关的小知识点：整体分为**六**几大类

- 前端浏览器相关

> Q1:   **浏览器到底是怎么渲染的** ？ **映射为前端常见的面试题是：当用户心情愉悦的打开浏览器时（输入URL） 发生了什么**

----



- 框架-Vue相关

> Q1:  **在Vue框架中，为什么尽量不要修改props**

> Q2: **如果不小心更改了，vue是怎么做的**

> Q3: **vue的双向绑定和vuex是否冲突**

> Q4: **vue的父组件和子组件的生命周期钩子执行的顺序**

---



- 原生JavaScript相关

> Q1:**使用sort() 对数组进行排序 - 【3,15,8,29,102,22】**

> Q2: **输出代码看结果** **为什么**

```js
var obj = {
    '2': 3,
    '3': 4,
    'length': 2,
    'splice': Array.prototype.splice,
    'push': Array.prototype.push
}
obj.push(1)
obj.push(2)
console.log(obj)


```

-----



- ES6新语法特性 - 箭头函数

> Q1：**箭头函数与普通函数（function）的区别是什么？**
>
> Q2: **构造函数（function）可以使用 new 生成实例，那么箭头函数可以吗？为什么**



----



- API性能

> Q1:**`a.b.c.d` 和 `a['b']['c']['d']`，哪个性能更高？**

> Q2:**数组里面有10万个数据，取第一个元素和第10万个元素的时间相差多少**

----



- 数据结构算法相关

> Q1: **已知数据格式，实现一个函数 fn 找出链条中所有的父级 id**



## 准备

- vue 的源码

```js
yarn add vue
```



- 一个测试小项目

## 00-已知数据格式，实现一个函数 fn 找出链条中所有的父级 id

![](https://raw.githubusercontent.com/yayxs/Pics/master/code.png)

> 有两种数据结构类似于数组， 

> 但在添加和删除元素时更为可控。它们就是栈和队列

### 栈 LIFO

**栈是一种遵从后进先出（LIFO）原则的有序集合。新添加的或待删除的元素都保存在栈的同一端，称作栈顶，另一端就叫栈底。在栈里，新元素都靠近栈顶，旧元素都接近栈底**

![](https://raw.githubusercontent.com/yayxs/Pics/master/Snipaste_2020-04-18_12-09-07.png)

- push(element(s))：添加一个（或几个）新元素到栈顶。 

- pop()：移除栈顶的元素，同时返回被移除的元素。 

- peek()：返回栈顶的元素，不对栈做任何修改（这个方法不会移除栈顶的 

元素，仅仅返回它）。 

- isEmpty()：如果栈里没有任何元素就返回true，否则返回false。 

- clear()：移除栈里的所有元素。 

- size()：返回栈里的元素个数。这个方法和数组的length属性很类似。

### 队列 FIFO

![](https://raw.githubusercontent.com/yayxs/Pics/master/Snipaste_2020-04-18_11-59-03.png)

- enqueue(element(s))：向队列尾部添加一个（或多个）新的项
- dequeue()：移除队列的第一（即排在队列最前面的）项，并返回被移除的元素
- front()：返回队列中第一个元素——最先被添加，也将是最先被移除的 元素。队列不做任何变动（不移除元素，只返回元素信息——与Stack类的 peek方法非常类似）
- isEmpty()：如果队列中不包含任何元素，返回true，否则返回false
- size()：返回队列包含的元素个数，与数组的length属性类似

### 广度优先搜索BFS

**广度优先搜索算法会从指定的第一个顶点开始遍历图，先访问其所有的相邻 点，就像一次访问图的一层。**

![Snipaste_2020-04-18_12-40-22.png](https://i.loli.net/2020/04/20/gw6WR1MC3bSloZN.png)

### 深度优先搜索DFS

**深度优先搜索算法将会从第一个指定的顶点开始遍历图，沿着路径直到这条路 径最后一个顶点被访问了，接着原路回退并探索下一条路径。换句话说，它是先深 度后广度地访问顶点**

![Snipaste_2020-04-18_12-43-19.png](https://i.loli.net/2020/04/20/lFRpSfsUI3niqGD.png)

| 算法         | 数据结构 |                      | 描述                                                         |
| ------------ | -------- | -------------------- | ------------------------------------------------------------ |
| 深度优先搜索 | 栈       | Depth-First Search   | 通过将顶点存入栈中，顶点是沿着路径被探索,存在新的相邻的顶点访问 |
| 广度优先搜索 | 队列     | Breadth-First Search | 通过将顶点存入队列中 最先入队列的顶点先被探索                |

## 01-输出以下代码执行的结果并解释为什么

```js
var obj = {
    '2': 3,
    '3': 4,
    'length': 2,
    'splice': Array.prototype.splice,
    'push': Array.prototype.push
}
obj.push(1)
obj.push(2)
console.log(obj)
```

### 类（伪）数组（arraylike）

- 就是像数组的对象（某些对象看起来像但不是）

- **通过索引属性访问元素**

- **拥有 length** 属性的对象

- underscore 中的定义

  ```js
  var MAX_ARRAY_INDEX = Math.pow(2, 53) - 1;
  var getLength = property('length');
  var isArrayLike = function(collection) {
    var length = getLength(collection);
    return typeof length == 'number' && length >= 0 && length <= MAX_ARRAY_INDEX; // 其中 JavaScript 中能精确表示的最大数字
  };
  ```

- **没有数组的方法**（push forEach）

```js
arrayLike.push('sex') // 01.js:20 Uncaught TypeError: arrayLike.push is not a function
```



#### 形式

```js

console.log(array[0]); // name
console.log(arrayLike[0]); // name

array[0] = "new name";
arrayLike[0] = "new name";
console.log(array[0]); // new name
console.log(arrayLike[0]); // new name
```

#### 间接调用

```js
Array.prototype.slice.call(arrayLike, 0); // ["name", "age", "sex"] 
```

#### 转为真正的数组

```js
Array.from(arrayLike); 
```

### 数组的push

- [mdn关于数组push](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/push)

>`push` 方法具有通用性。该方法和 [`call()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call) 或 [`apply()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) 一起使用时，可应用在类似数组的对象上。`push` 方法根据 `length` 属性来决定从哪里开始插入给定的值。如果 `length` 不能被转成一个数值，则插入的元素索引为 0，包括 `length` 不存在时。当 `length` 不存在时，将会创建它。

> 唯一的原生类数组（array-like）对象是 [`Strings`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String)，尽管如此，它们并不适用该方法，因为字符串是不可改变的。

**大白话**

其实push的时候会首先查询数组（伪数组）的 length 属性，接着在数组的最后一个添加上新的元素即 arr[length]

```js
var testObj = {
  "2": 3,
  "3": 4,
  length: 2,
  push: Array.prototype.push,
};


testObj.push(1) 
console.log(testObj) //// {2: 1, 3: 4, length: 3, push: ƒ}
testObj.push(2)
console.log(testObj) //{2: 1, 3: 2, length: 4, push: ƒ}
```

- 第一点就是每次 push  后 length 会加1

![00.png](https://i.loli.net/2020/04/20/FthL2egVXTCy6vk.png)

### 'splice': Array.prototype.splice



- [在对象上加splice](https://github.com/ChromeDevTools/devtools-frontend/blob/master/front_end/event_listeners/EventListenersUtils.js#L330)

```js
 /**
     * @param {?Object} obj
     * @return {boolean}
     */
    function isArrayLike(obj) {
      if (!obj || typeof obj !== 'object') {
        return false;
      }
      try {
        if (typeof obj.splice === 'function') {
          const len = obj.length;
          return typeof len === 'number' && (len >>> 0 === len && (len > 0 || 1 / len > 0));
        }
      } catch (e) {
      }
      return false;
    }
```

**为什么对象添加了splice属性后并没有调用就会变成类数组对象这个问题，这是控制台中 DevTools 猜测类数组的一个方式**

- 存在且是对象
- 对象上的`splice` 属性是函数类型
- 对象上有 `length` 属性且为正整数



## 02-使用sort() 对数组进行排序 - 【3,15,8,29,102,22】

> [mdn 上的sort](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

**`sort()` 方法用[原地算法](https://en.wikipedia.org/wiki/In-place_algorithm)对数组的元素进行排序，并返回数组。默认排序顺序是在将元素转换为字符串，然后比较它们的UTF-16代码单元值序列时构建的**

- 原地算法[原地算法](https://en.wikipedia.org/wiki/In-place_algorithm)
- 将元素转为字符串
- UTF-16

![00.png](https://i.loli.net/2020/04/20/E258fou79vS3iVa.png)

采用的`utf-16` ,常见的字符`数字` `英语大小写` `汉字`

```js
let arrs = ['你好啊','HELLO','hello',666]
arrs.sort()
console.log(arrs)  // [666, "HELLO", "hello", "你好啊"]
```

**总结**

数字》英语大写》英语小写》汉字

````js
	/**
     * Sorts an array.
     * @param compareFn Function used to determine the order of the elements. It is expected to return
     * a negative value if first argument is less than second argument, zero if they're equal and a positive
     * value otherwise. If omitted, the elements are sorted in ascending, ASCII character order.
     * ```ts
     * [11,2,22,1].sort((a, b) => a - b)
     * ```
     */
    sort(compareFn?: (a: T, b: T) => number): this;
````



- 阮老师 [字符编码](http://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html)

- 步骤

  - 转为字符串 数字>英语大写>英语小写>汉字

  ![01.png](https://i.loli.net/2020/04/20/TwdWu5JmsyOSniC.png)

  - 对比第一个字符===>15 102 29 22 3 8
  - 对比第二个字符===>102 15 22 29 3 8
  - 对比第三个字符===>102 15 22 29 3 8

- 案例

```js
arr.sort((x, y) => {
  console.log(`排序：${x}----${y}`);
});
```

```
排序：15----3
排序：8----15
排序：29----8
排序：102----29
排序：22----102
```

```js
arr.sort((x, y) => {
  console.log(`${x}-${y}=${x - y}`);
});
```

```
15-3=12
8-15=-7
29-8=21
102-29=73
22-102=-80
```

```js
arr.sort((x, y) => {
  console.log(`${x}-${y}=${x - y}`);
  return x - y;
});
console.log(arr);
```

```
15-3=12
8-15=-7
8-15=-7
8-3=5
29-8=21
29-15=14
102-15=87
102-29=73
22-15=7
22-102=-80
22-29=-7
[ 3, 8, 15, 22, 29, 102 ]
```

- 总结
  - 返回值小于 0 x 移动到 y 前 升序 return x-y
  - 返回值大于 0 x 移动到 y 后 降序 return y-x
  - 返回值等于 0 大多浏览器相对不变
- 结果：

> [ 102, 15, 22, 29, 3, 8 ]

## 03-关于箭头函数

>**Q5: 箭头函数与普通函数（function）的区别是什么？构造函数（function）可以使用 new 生成实例，那么箭头函数可以吗？为什么？**

- [mdn-箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

- [阮老师es6-箭头函数]([https://es6.ruanyifeng.com/#docs/function#%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0](https://es6.ruanyifeng.com/#docs/function#箭头函数))

### 什么是箭头函数

- 语法简洁
- 没有自己的this
- **不能用作构造函数。**

```js
const agesArr = [12,13,7,8 ]

const res = agesArr.map(item=>`${item}岁`)
console.log(res) // [ '12岁', '13岁', '7岁', '8岁' ]
```

```js
const fn  = ([a, b] = [1, 2], {x: c} = {x: a + b}) => a + b + c;
const res1 = fn()
console.log(res1) // 6
```

### 优势

- 写起来更短
- 没有单独的`this`
- 箭头函数使得表达更加简洁。

### 没有箭头函数

**函数是根据如何被调用来定义这个函数的`this`**

- 如果是该函数是一个构造函数，this指针指向一个新的对象
- 在严格模式下的函数调用下，this指向undefined

```js
 function Person() {
        // Person() 构造函数定义 `this`作为它自己的实例.
        this.age = 0;

        setInterval(function growUp() {
          console.log(this);
          // 在非严格模式, growUp()函数定义 `this`作为全局对象,
          // 与在 Person()构造函数中定义的 `this`并不相同.
            // 此时的this是window 对象（浏览器环境）
          this.age++;
        }, 1000);
      }
```

### 用箭头函数

```js
function Person(){
  this.age = 0;

  setInterval(() => {
    this.age++; // |this| 正确地指向 p 实例
  }, 1000);
}

var p = new Person();
```

**箭头函数不会创建自己的`this,它只会从自己的作用域链的上一层继承this`**



### JavaScript中的new操作符

#### 面试题

根据`new操作符`相关的知识点一般会 延伸出以下的**面试题** ，面试官你是否有很多问号

- 问题一：new 之后都做了些什么？？
- 问题二：能否手写new操作符原理？？

[mdn关于new运算符关键字的描述](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new)

>1. 创建一个空的简单JavaScript对象（即`{}`）；
>2. 链接该对象（即设置该对象的构造函数）到另一个对象 ；
>3. 将步骤1新创建的对象作为`this`的上下文 ；
>4. 如果该函数没有返回对象，则返回`this`。

以上4条是`MDN` 上关于new 操作符（或者说关键字）的面试，简单的来体验下利用构造函数来`new` 一个对象

```js
var self;

function Person(name) {
  console.log(this);
  self = this;
  this.name = name;
}
let p = new Person("张三");
console.log(p);
console.log(self === p); // true 构造函数中的this 绑定在了p这个对象上
console.log(p.__proto__ === Person.prototype); // 对象p的原型属性指向构造函数的原型，这样也就保证了实例能够访问在构造函数原型中定义的属性和方法。
```

然后在**构造函数添加原型方法**

```js
function Persion(name){
    this.name = name
}
console.log(Persion.prototype)
Persion.prototype.sayHello = function(){
    console.log(this) // 指向构造出的对象
    console.log(this.name) // 小明
}

let xiaoMing = new Persion('小明')
xiaoMing.sayHello()
```

经过上文的简单案例我们可以得知，

- `new` 一个构造函数得到一个对象，它的原型属性（也就是__ proto __）与该构造函数的原型是全等

- ` new` 通过构造函数 `Persion` 创建出来的实例可以访问到构造函数中的属性,就行这样

  ```js
  console.log(xiaoMing.name) // 小明
  ```

- 言简意赅：new出来的实例对象通过原型链和构造函数联系起来

**构造函数说白了也是一个函数，那是函数就可以有返回值**

```js
function Person(name) {
  this.name = name;
  //   return 1; // 返回内部新创建的对象
  //   return "1"; // 返回内部新创建的对象
  // return null; // 返回内部新创建的对象
  //   return undefined; // 返回内部新创建的对象
  //   return {}; // {} // 直接返回
  return function () {}; // 直接返回
  return [1]; // [1] // 直接返回
}
let p = new Person("李四");
console.log(p);
```

有了给构造函数返回一个值得想法，那就通过不同的`数据类型` 进行测试得出结论

- 不同的数据类型返回的效果是不一样的，像数字1 字符串”1“ ，返回的依然是内部创建的对象
- **那如果返回一个对象（{}）或者说数组（【】）** 都会直接返回回去

#### 小结

也就是说，构造函数一般不需要`return ` 

- 返回一般的数据类型吧，不起作用
- 返回对象吧， new 的意义又何在呢

#### 手写一个自己的myNew

如果自己实现一个new 的话，首先要满足它的几点效果

1. 一个构造函数会返回一个对象，那函数里就应该有对象

   ```js
   let obj ={}
   ```

2. 并将其`__proto__`属性指向构造函数的`prototype`属性

   ```js
   obj.__proto__ = constructor.prototype;
   ```

3. 调用构造函数，绑定this

   ```js
   constructor.apply(obj, args)
   ```

4. 返回原始值需要忽略，返回对象需要正常处理

   ```js
   res instanceof Object ? res : obj
   ```

#### 测试成果

```

function myNew() {
  let [constructor, ...args] = [...arguments];
  let obj = {};
  obj.__proto__ = constructor.prototype;

  let res = constructor.apply(obj, args);
  return res instanceof Object ? res : obj;
}

function Person(name) {
  this.name = name;
//   return {};
}

Person.prototype.sayHi = function () {
  console.log(`原型方法中的函数--${this.name}`);
};
let p1 = myNew(Person, "测试");
// console.log(p1)
p1.sayHi();
console.log(p1.name);
```





### 箭头函数使用`new`

```js
 var Foo = () => {};
      var foo = new Foo(); // TypeError: Foo is not a constructor
```

- 不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误



## 04-`a.b.c.d` 和 `a['b']['c']['d']`，哪个性能更高？



----

## 04-vue 生命周期进阶

### 基本流程

![](https://cn.vuejs.org/images/lifecycle.png)



- new vue 创建实例
- 初始化事件 生命周期
- **beforeCreate**
- 初始化 注入校验
- **created**
- 是否指定 el
  - 否： 调用 vm.$mount(el)
  - 是：是否指定template
    - 否 将el 外部的html 作为template 编译
    - 是 将 template 编译到render
- **beforeMount**
- 创建vm.$el 并用其替换el
- **mounted**
- 挂载完毕
- 当data 修改的时候：
  - **beforeUpdate**
  - **updated**
- 调用vm.$destroy()
- **beforeDestroy**
- 解除绑定 销毁子组件 事件监听
- 销毁完毕
- **destroyed**

### 加载渲染的过程

![](https://raw.githubusercontent.com/yayxs/Pics/master/20200421213852.png)

**父组件挂载完毕肯定是等里面的子组件都挂载完毕后才算父组件挂载完毕了，所以父组件的mounted在最后。**

### 子组件更新过程

子组件更新过程(子组件更新影响到父组件的情况)：`父beforeUpdate -> 子beforeUpdate->子updated -> 父updted`
子组件更新过程(子组件更新不影响父组件的情况)：`子beforeUpdate -> 子updated`

### 父组件更新过程

![20200421221422](https://raw.githubusercontent.com/yayxs/Pics/master/img/20200421221422.png)

**eactivated函数的触发时间是在视图更新时触发。因为当视图更新时才能知道keep-alive组件被停用了。**

父组件更新过程(父组件影响子组件的情况)：`父beforeUpdate -> 子beforeUpdate->子updated -> 父updted`
父组件更新过程(父组件不影响子组件的情况)：`父beforeUpdate -> 父updated`

### 销毁过程

父beforeDestroy->子beforeDestroy->子destroyed->父destroyed

#### 小补充

| deactivated | keep-alive 组件停用时调用。 |
| ----------- | --------------------------- |
| activated   | keep-alive 组件激活时调用。 |

### 总结

Vue父子组件生命周期钩子的执行顺序遵循：从外到内，然后再从内到外，不管嵌套几层深，也遵循这个规律
Vue父子组件生命周期钩子的执行顺序遵循：从外到内，然后再从内到外，不管嵌套几层深，也遵循这个规律


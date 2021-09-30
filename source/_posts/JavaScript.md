---
title: JavaScript
date: 2021-02-09 18:53:06
tags:
categories: JavaScript
---

<meta name="referrer" content="no-referrer"/>
JavaScript 是互联网上最流行的脚本语言，这门语言可用于 HTML 和 web，更可广泛用于服务器、PC、笔记本电脑、平板电脑和智能手机等设备。

<!-- more -->

为什么起名叫JavaScript？原因是当时Java语言非常红火，所以网景公司希望**借Java的名气来推广**，但事实上JavaScript除了语法上有点像Java，其他部分基本上没啥关系。

JavaScript语言是在10天时间内设计出来的，虽然语言的设计者水平非常NB，但谁也架不住“时间紧，任务重”，所以，JavaScript有很多设计缺陷

# 快速入门

JavaScript**严格区分大小写**，如果弄错了大小写，程序将报错或者运行不正常。

## 数据类型和变量

JavaScript不区分整数和浮点数，统一用**Number**表示。

**比较运算符**

第一种是`==`比较，它会**自动转换数据类型**再比较，很多时候，会得到非常诡异的结果；

第二种是`===`比较，它不会自动转换数据类型，如果数据类型不一致，返回`false`，如果一致，再比较。

由于JavaScript这个设计缺陷，不要使用`==`比较，始终坚持使用`===`比较。



这种变量本身类型不固定的语言称之为动态语言，与之对应的是静态语言，Java是静态语言。

```javascript
var a = 123; // a的值是整数123
a = 'ABC'; // a变为字符串
```



alert()

console.log()

## 字符串

多行字符串：反引号``

模板字符串

```javascript
var name = "world";
var message = `hello ${name}`; // 反引号
```

## 数组

JavaScript的`Array`可以包含任意数据类型，并通过索引来访问每个元素。

```javascript
var arr = [1, 2, 3.14, 'Hello', null, true];
arr.length = 2; // arr变为[1, 2]
```

indexOf

slice: 对应String的`substring()`

push和pop: `pop()`则把`Array`的最后一个元素删除掉

unshift和shift: 如果要往`Array`的头部添加若干元素，使用`unshift()`方法，`shift()`方法则把`Array`的第一个元素删掉

sort

reverse

splice

`splice()`方法是修改`Array`的“万能方法”，它可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素：

```javascript
var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
// 从索引2开始删除3个元素,然后再添加两个元素:
arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
```

concat: 拼接Array

join：把当前`Array`的每个元素都用指定的字符串连接起来，然后返回连接后的字符串

```javascript
var arr = ['A', 'B', 'C', 1, 2, 3];
arr.join('-'); // 'A-B-C-1-2-3'

alert(`欢迎${arr.slice(0,3)}和${arr[3]}同学！`);
```

## 对象

JavaScript的对象是动态类型，可以自由地给一个对象添加或删除属性

检测`xiaoming`是否拥有某一属性，可以用`in`操作符

```javascript
var xiaoming = {
    name: '小明'
};
delete xiaoming.age;
'toString' in xiaoming
```

## 循环

`for ... in`对`Array`的循环得到的是`String`而不是`Number`。

```javascript
var arr = ['A', 'B', 'C'];
for (var i in arr) {
    console.log(i); // '0', '1', '2'
    console.log(arr[i]); // 'A', 'B', 'C'
}
```

## Map和Set

```javascript
var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
var s = new Set([1, 2, 3, 3, '3']);
```

## iterable

遍历`Array`可以采用下标循环，遍历`Map`和`Set`就无法使用下标。为了统一集合类型，ES6标准引入了新的`iterable`类型，`Array`、`Map`和`Set`都属于`iterable`类型。

```javascript
for (var x of arr)
    
arr.forEach(function (element, index, array)
```

# 函数

借助抽象，我们才能不关心底层的具体计算过程，而直接在更高的层次上思考问题。

## 函数定义和调用

`function abs(x){}`等价于`var abs = function(x){};`

arguments

它只在函数内部起作用，并且永远指向当前函数的调用者传入的所有参数。

JavaScript引擎有一个在行末自动添加分号;的机制

## 变量作用域与解构赋值

全局作用域

不在任何函数内定义的变量就具有全局作用域。实际上，JavaScript默认有一个全局对象`window`，全局作用域的变量被绑定到`window`的一个属性。如`window.alert()`

名字空间

全局变量会绑定到`window`上，不同的JavaScript文件如果使用了相同的全局变量，或者定义了相同名字的顶层函数，都会造成命名冲突，并且很难被发现。

减少冲突的一个方法是把自己的所有变量和函数全部绑定到一个全局变量中。如：

```javascript
// 唯一的全局变量MYAPP:
var MYAPP = {};

// 其他变量:
MYAPP.name = 'myapp';
MYAPP.version = 1.0;

// 其他函数:
MYAPP.foo = function () {
    return 'foo';
}
```

解构赋值：直接对多个变量同时赋值

`let [x, [y, z]] = ['hello', ['JavaScript', 'ES6']];`

## 方法

在一个对象中绑定函数，称为这个对象的方法。

## 高阶函数

JavaScript的函数其实都指向某个变量。既然变量可以指向函数，函数的参数能接收变量，那么**一个函数就可以接收另一个函数作为参数**，这种函数就称之为高阶函数。

```javascript
function add(x, y, f) {
    return f(x) + f(y);
}
var x = add(-5, 6, Math.abs); // 11
```

map/reduce

map是对数组的每个元素分别计算。

Array的`reduce()`把一个函数作用在这个`Array`的`[x1, x2, x3...]`上，这个函数必须接收两个参数，`reduce()`把结果继续和**序列的下一个元素**做**累积**计算。

```javascript
[x1, x2, x3, x4].reduce(f) = f(f(f(x1, x2), x3), x4)
```

filter

```javascript
var arr = [1, 2, 4, 5, 6, 9, 10, 15];
var r = arr.filter(function (x) {
    return x % 2 !== 0;  // 保留奇数
});
```

sort

### Array

`every()`方法可以判断数组的所有元素是否满足测试条件。

`find()`方法用于查找符合条件的第一个元素，如果找到了，返回这个元素，否则，返回undefined

`findIndex()`返回符合条件的第一个元素的索引

`forEach()`和`map()`类似，它也把每个元素依次作用于传入的函数，但不会返回新的数组。`forEach()`常用于遍历数组，因此，传入的函数不需要返回值。`arr.forEach(console.log);`

## 闭包


---
title: JavaScript
date: 2021-02-09 18:53:06
tags:
categories:
---

<meta name="referrer" content="no-referrer"/>
<!-- more -->

为什么起名叫JavaScript？原因是当时Java语言非常红火，所以网景公司希望**借Java的名气来推广**，但事实上JavaScript除了语法上有点像Java，其他部分基本上没啥关系。

JavaScript语言是在10天时间内设计出来的，有很多设计缺陷。

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




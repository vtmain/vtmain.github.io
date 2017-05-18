---
title: javascript变量、数据类型
date: 2017-05-11 15:05:52
updated:
description:
tags: [JavaScript]
categories: [JavaScript]
toc: false
---

**一、变量**   
ECMAScript的变量是松散类型的，所谓松散类型就是可以用来保存任何类型的数据。每个变量仅仅是一个用于保存值的占位符而已。

<!-- more -->

```js
var message_un;      // 声明，但未初始化
var message = "hi";  // 可在声明同时初始化
message = 100;       // 已有类型时，转其他类型。有效，但不推荐

// 下面这个变量并没有声明;
// var age;

function test(){
    var a = "hi";    // 局部变量
    b = "hello";     // 全局变量

    var c = "name",  // 可连续初始化多个变量类型，注意间隔逗号
        d = false,
        e = 29;
}
test();
alert(a);                        // 错误！
alert(message_un);               // 错误！
alert(message_un == undefined);  // true
alert(b);                        // "hello"
alert(c);                        // "name"
alert(d);                        // false
alert(e);                        //
alert(age);                      // 错误！
```

**二、数据类型**  
5种简单数据类型（基本数据类型）   
`Undefined`、`Null`、`Boolean`、`Number`、`String`  
1种复杂数据类型  
`Object`  

**Undefined** 类型只有一个值，即特殊的undefined。在使用`var`声明变量但未对其加以初始化时，这个变量的值就是undefined，比如上面定义的`message_un`。  
**Null** 类型是第二个只有一个值的数据类型，这个特殊的值是`null`。从逻辑角度看，null值表示一个空对象指针，而这也正是`typeof null`会返回`object`的原因。

```js
var n1 = 95;
var car = null;
alert(typeof message_un);  // "undefined"
alert(typeof age);         // "undefined"
alert(typeof message);     // "string"
alert(typeof(message));    // "string"
alert(typeof 95);          // "number"
alert(typeof(n1));         // "number"
alert(typeof(d));          // "boolean"
alert(typeof null);        // "object"
alert(typeof car);         // "object"
```

如果定义的变量准备在将来用于保存对象，那么最好将该变量初始化为`null`而不是其他值。这样一来，只要直接检查null值就可以知道对应的变量是否已经保存了一个对象的引用。

```js
if (car != null) {
    // do something
}

// 实际上undefined值是派生自null值的，因此相等性测试要返回true
alert(null == undefined);   // true
```
虽然`==`总是返回true，但仍需明确`undefined`和`null`的区别，二者用途完全不同。
- 没必要把一个变量的值显式设置为undefined，因为不初始化时即为undefined
- 只要意在保存对象的变量还没有真正保存对象，就应该明确地让该变量保存null值  

这样做不仅体现null作为空对象指针的惯例，而且也有助于进一步区分undefined和null。

**Boolean** 类型只有两个字面值true和false。这两个值与数字值不是一回事，true不一定等于1，false不一定等于0。ECMAScript中所有类型的值都有与这两个Boolean值等价的值。要转换，可以调用转型函数Boolean()  
```js
var message = "hello world";
var messageAsBoolean = Boolean(message);   // true
```
转换值取决于数据类型及其实际值，如下表  

| 数据类型 | 转换为true的值 | 转换为false的值 |  
|:--------|:------------------------|:---------------|  
|Boolean |true |false |  
|String |任何非空字符串 |""(空字符串) |  
|Number |任何非零数字值(包括无穷大) |0和NaN |  
|Object |任何对象 |null |  
|Undefined|n/a |undefined |  

　　
待续..

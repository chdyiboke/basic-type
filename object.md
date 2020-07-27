# object


## ES6 Object.is()

`Object.is(value1, value2)`
比较 value1 和 value2 是否相等


```
Object.is('foo', 'foo');     // true
Object.is(window, window);   // true

Object.is('foo', 'bar');     // false
Object.is([], []);           // false

var foo = { a: 1 };
var bar = { a: 1 };
Object.is(foo, foo);         // true
Object.is(foo, bar);         // false

Object.is(null, null);       // true

// 特例
Object.is(0, -0);            // false
Object.is(-0, -0);           // true
Object.is(NaN, 0/0);         // true

```
和  ‘===’ 一些不同之处

```
// 使用 ‘===’
+0 === -0 //true
NaN === NaN // false
// 使用 Object.is()
Object.is(+0, -0) // false
Object.is(NaN, NaN) // true

```


严格 比较对象的3种方式：

1. 相等（==）符号
2. 全等（===）符号
3. Object.js()

松散比较：
浅比较（单层对象进行比较）
对象属性比较。

深比较
递归 或者  JSON.stringify



# 数组

## 深入理解数组类型

在Js中数组存在两种形式：  
一种是与C/C++等相同的在`连续内存`中存放数据的快数组，另一种是`HashTable`结构的慢数组.


```
var arr = []; // 快数组
var arr = Array(100);
var arr = new Array(100);
```

在V8引擎中，直接创建数组默认的方式是创建`快数组`，会直接为数组开辟一定大小的内存。


大小转化主要和数组大小有关系

### 快数组==>慢
```
快数组转换为慢数组主要有以下两种情况：

当新容量大于等于3 * 3倍的扩容后的容量，会转变为慢数组。
当加入的索引值index比当前容量capacity差值大于等于1024 时，也就是至少有1024个HOLEY时，即会转为慢数组，例如定义一个长度为1的数组arr然后使用arr[2000]=1赋值，此时数组就会被转换为慢数组。
```

### 慢数组==>快
```
当慢数组的元素可存放在快数组中且长度小于Smi::kMaxValue且对于快数组仅节省了50%的空间，则会转变为快数组。
```
### 对比

```
对于快慢数组，两者的也有各自的特点，在实际使用的过程中是存在相互转换的，在存储方式、内存使用、遍历效率方面有如下总结：

存储方式方面：快数组内存中是连续的，慢数组在内存中是零散分配的。
内存使用方面：由于快数组内存是连续的，可能需要开辟一大块供其使用，其中还可能有很多空洞，是比较费内存的。慢数组不会有空洞的情况，且都是零散的内存，比较节省内存空间。
遍历效率方面：快数组由于是空间连续的，遍历速度很快，而慢数组每次都要寻找key 的位置，遍历效率会差一些。

```

## forEach 和 map

```

let arr = [1,2,3,3,3];
let foreachArr = arr.forEach((x,index) => arr[index]=2*x);  
// undefined   [2, 4, 6, 6, 6] arr的值被修改

let mapArr = arr.map((x,index) => arr[index]=2*x);  
// [2, 4, 6, 6, 6]   [2, 4, 6, 6, 6]  arr的值被修改
console.log(arr, mapArr);
// forEach 无返回值 ， map有返回值（新数组占内存）

上面 arr 是引用类型，当然被修改了。

```

### 实现一个map

```
Array.prototype.map1 = function (callback){	
	let newArr = [];
	let that = this;
	for(let i=0;i<that.length;i++){		
		newArr.push(callback(that[i])); // 未考虑深拷贝
	}
	return newArr;
}

```

## splice 和 slice


第二个参数的意义：
```
var arr=[0,1,2,3,4,5,6,7,8,9];//设置一个数组
console.log(arr.slice(2,7));//2,3,4,5,6
console.log(arr.splice(2,7));//2,3,4,5,6,7,8
//由此我们简单推测数量两个函数参数的意义,
slice(start,end)第一个参数表示开始位置,第二个表示截取到的位置(不包含该位置)
splice(start,length)第一个参数开始位置,第二个参数截取长度


```

splice修改原数组：
```
var x=y=[0,1,2,3,4,5,6,7,8,9]
console.log(x.slice(2,5));//2,3,4
console.log(x);[0,1,2,3,4,5,6,7,8,9]原数组并未改变
//接下来用同样方式测试splice
console.log(y.splice(2,5));//2,3,4,5,6
console.log(y);//[0,1,7,8,9]显示原数组中的数值被剔除掉了

```

## 数组的原型是数组

```
Array.isArray( Array.prototype )

答案：true
解析：Array.prototype是一个数组
数组的原型是数组，对象的原型是对象，函数的原型是函数

Function.prototype.__proto__ ===    Array.prototype.__proto__ === Object.prototype  // 这就是原型链
```

```
//man 对象

const  man = new Person();

一：基本概念
prototype(只有方法才有，是属性的集合,使您有能力向对象添加属性和方法。) 
_proto_(每个对象都有，指向原型对象的指针，指针链就是原型链)

一：两条原型链
function Person(){

}
var man = new Person();
Person.prototype.name='cy'
man._proto_    指向   Person.prototype

Person.prototype._proto_   指向  Object.prototype
Object.prototype._proto_   = null   (终点)

一：构造函数执行
constructor（指向构造函数）

Person.prototype.constructor 指向 Person
Object.prototype.constructor 指向 Object

```


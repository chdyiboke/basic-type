# 数组


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





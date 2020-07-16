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






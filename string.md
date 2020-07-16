# string
https://www.runoob.com/jsref/jsref-obj-string.html


## replace 替换

不修改原字符串：
```
var str="Visit Microsoft! Visit Microsoft!";
var n=str.replace("Microsoft","Runoob");

// n: Visit Runoob!Visit Microsoft!
```

正则：

执行一个全局替换例子:

```
var str="Mr Blue has a blue house and a blue car";
var n=str.replace(/blue/g,"red");
// n: Mr Blue has a red house and a red car
```

如果是传参数：new RegExp

```
String.prototype.replaceAll = function(search, replacement) {
    var target = this;
    return target.replace(new RegExp(search, 'g'), replacement);
};

```

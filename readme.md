## 题目描述

找出元素 item 在给定数组 arr 中的位置

## 输出描述:

```
如果数组中存在 item，则返回元素在数组中的位置，否则返回 -1
```

示例1

## 输入

```
[ 1, 2, 3, 4 ], 3
```

## 输出

```
2
```

答案：

```
function indexOf(arr, item) {
  if (Array.prototype.indexOf){
      return arr.indexOf(item);
  } else {
      for (var i = 0; i < arr.length; i++){
          if (arr[i] === item){
              return i;
          }
      }
  }     
  return -1;
}
```



------

## 题目描述

计算给定数组 arr 中所有元素的总和

## 输入描述:

```
数组中的元素均为 Number 类型
```

示例1

## 输入

```
[ 1, 2, 3, 4 ]
```

## 输出

```
10
```



```
不考虑算法复杂度，用递归做：
function sum(arr) {
    var len = arr.length;
    if(len == 0){
        return 0;
    } else if (len == 1){
        return arr[0];
    } else {
        return arr[0] + sum(arr.slice(1));
    }
}
常规循环：
function sum(arr) {
    var s = 0;
    for (var i=arr.length-1; i>=0; i--) {
        s += arr[i];
    }
    return s;
}
函数式编程 map-reduce：
function sum(arr) {
    return arr.reduce(function(prev, curr, idx, arr){
        return prev + curr;
    });
}
数组方法 reduce 用来迭代一个数组，并且把它累积到一个值中。

使用 reduce 方法时，你要传入一个回调函数，这个回调函数的参数是一个 累加器 （比如例子中的 previousVal) 和当前值 (currentVal）。

reduce 方法有一个可选的第二参数，它可以被用来设置累加器的初始值。如果没有在这定义初始值，那么初始值将变成数组中的第一项，而 currentVal 将从数组的第二项开始。
idx:可选。当前元素的索引
reduce()使用说明：http://www.runoob.com/jsref/jsref-reduce.html

forEach遍历：
function sum(arr) {
    var s = 0;
    arr.forEach(function(val, idx, arr) {
        s += val;
    }, 0);
  
    return s;
};
这里是forEach(fun , thisValue), thisValue不传时为undefined，一般传this，那么内部this指向window
eval：
function sum(arr) {
    return eval(arr.join("+"));
};
```

------

## 题目描述

移除数组 arr 中的所有值与 item 相等的元素。不要直接修改数组 arr，结果返回新的数组

示例1

## 输入

```
[1, 2, 3, 4, 2], 2
```

## 输出

```
[1, 3, 4]
```

```
1.splice()
function remove(arr,item){
    var newarr = arr.slice(0);
    for(var i=0;i<newarr.length;i++){
        if(newarr[i] == item){
            newarr.splice(i,1);
            i--;
        }
    }
    return newarr;
}

2.push()
function remove(arr,item){
    var newarr = [];
    for(var i=0;i<arr.length;i++){
        if(arr[i] != item){
            newarr.push(arr[i]);
        }
    }
    return newarr;
}

3.Array.prototype.filter()
function remove(arr,item){
    return arr.filter(function(ele){
         return ele != item;
    })
}
```

------

## 题目描述

移除数组 arr 中的所有值与 item 相等的元素，直接在给定的 arr 数组上进行操作，并将结果返回

示例1

## 输入

```
[1, 2, 2, 3, 4, 2, 2], 2
```

## 输出

```
[1, 3, 4]
```

```
function removeWithoutCopy(arr, item) {
    for(var i=0;i<arr.length;i++){
        if(arr[i] == item){
            arr.splice(i,1);
            i--;
        }
    }
    return arr;
}

function removeWithoutCopy(arr, item) {
    var n=arr.length;
     for(var i=0;i<n;i++){
         if(arr[0]!==item)   
             arr.push(arr[0]);
         arr.shift();
           
    }
    return arr;
}
如果数组第一个元素 != item 那么把它加入到数组末尾，然后开头的自己出栈；
```

------

## 题目描述

在数组 arr 末尾添加元素 item。不要直接修改数组 arr，结果返回新的数组

示例1

## 输入

```
[1, 2, 3, 4],  10
```

## 输出

```
[1, 2, 3, 4, 10]
```

```
//普通的迭代拷贝
function append(arr, item) {
	var length = arr.length,
	newArr = []; 
	for (var i = 0; i < length; i++) {
		newArr.push(arr[i]);
	}
	newArr.push(item);
	return newArr;
}

//使用slice浅拷贝+push组合
function append(arr, item) {
	var newArr = arr.slice(0);
    newArr.push(item);
    return newArr;
}

//使用concat将传入的数组或非数组值与原数组合并,组成一个新的数组并返回
function append(arr, item) {
	return arr.concat(item);
}


```

------

## 题目描述

删除数组 arr 最后一个元素。不要直接修改数组 arr，结果返回新的数组

示例1

## 输入

```
[1, 2, 3, 4]
```

## 输出

```
[1, 2, 3]
```



```
//利用slice
function truncate(arr) {
    return arr.slice(0,-1);
}
//利用filter
function truncate(arr) {
    return arr.filter(function(v,i,ar) {
        return i!==ar.length-1;
    });
}
//利用push.apply+pop
function truncate(arr) {
    var newArr=[];
    [].push.apply(newArr, arr);
    newArr.pop();
    return newArr;
}
//利用join+split+pop    注意！！！：数据类型会变成字符型
function truncate(arr) {
    var newArr = arr.join().split(',');
    newArr.pop();
    return newArr;
}
//利用concat+pop
function truncate(arr) {
    var newArr = arr.concat();
    newArr.pop();
    return newArr;
}
//普通的迭代拷贝
function truncate(arr, item) {
    var newArr=[];
    for(var i=0;i<arr.length-1;i++){
        newArr.push(arr[i]);
    }
    return newArr;
}
```

------

## 题目描述

在数组 arr 开头添加元素 item。不要直接修改数组 arr，结果返回新的数组

示例1

## 输入

```
[1, 2, 3, 4], 10
```

## 输出

```
[10, 1, 2, 3, 4]
```

```
//concat()  简单粗暴
function prepend(arr, item) {
       return [item].concat(arr);
}

//unshift()
function prepend(arr, item) {
     //将arr数组复制给a
     var a = arr.slice(0);
     //使用unshift方法向a开头添加item
     a.unshift(item);
     return a;
 }
```

------

## 题目描述

删除数组 arr 第一个元素。不要直接修改数组 arr，结果返回新的数组

示例1

## 输入

```
[1, 2, 3, 4]
```

## 输出

```
[2, 3, 4]
```

```
//简单粗暴
function curtail(arr) {
    return arr.slice(1);
}

//利用filter
function curtail(arr) {
    return arr.filter(function(v,i) {
        return i!==0;
    });
}
//利用push.apply+shift
function curtail(arr) {
    var newArr=[];
    [].push.apply(newArr, arr);
    newArr.shift();
    return newArr;
}
//利用join+split+shift    注意！！！：数据类型会变成字符型
function curtail(arr) {
    var newArr = arr.join().split(',');
    newArr.shift();
    return newArr;
}
//利用concat+shift
function curtail(arr) {
    var newArr = arr.concat();
    newArr.shift();
    return newArr;
}
//普通的迭代拷贝
function curtail(arr) {
    var newArr=[];
    for(var i=1;i<arr.length;i++){
        newArr.push(arr[i]);
    }
    return newArr;
}

```



------


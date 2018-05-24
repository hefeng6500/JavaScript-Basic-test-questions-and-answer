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

## 题目描述

合并数组 arr1 和数组 arr2。不要直接修改数组 arr，结果返回新的数组

示例1

## 输入

```
[1, 2, 3, 4], ['a', 'b', 'c', 1]
```

## 输出

```
[1, 2, 3, 4, 'a', 'b', 'c', 1]
```

```
//concat() 简单粗暴
function concat(arr1, arr2) {
    return arr1.concat(arr2)
}

//利用slice+push.apply
function concat(arr1, arr2) {
    var newArr=arr1.slice(0);
    [].push.apply(newArr, arr2);
    return newArr;
}
//利用slice+push
function concat(arr1, arr2) {
    var newArr=arr1.slice(0);
    for(var i=0;i<arr2.length;i++){
        newArr.push(arr2[i]);
    }
    return newArr;
}
//普通的迭代拷贝
function concat(arr1, arr2) {
    var newArr=[];
    for(var i=0;i<arr1.length;i++){
        newArr.push(arr1[i]);
    }
    for(var j=0;j<arr2.length;j++){
        newArr.push(arr2[j]);
    }
    return newArr;
}
```



------

## 题目描述

在数组 arr 的 index 处添加元素 item。不要直接修改数组 arr，结果返回新的数组

示例1

## 输入

```
[1, 2, 3, 4], 'z', 2
```

## 输出

```
[1, 2, 'z', 3, 4]
```

```
function insert(arr, item, index) {
     //复制数组
     var a = arr.slice(0);
     a.splice(index, 0, item);
     return a;
 }
```

------

## 题目描述

统计数组 arr 中值等于 item 的元素出现的次数

示例1

## 输入

```
[1, 2, 4, 4, 3, 4, 3], 4
```

## 输出

```
3
```

```

function count(arr, item) {
     var count = 0;
     arr.forEach(function(e){
         //e为arr中的每一个元素，与item相等则count+1
         e == item ? count++ : 0;
     });
     return count;
 }
 

function duplicates(arr) {
 var result = [];
    arr.forEach(function(elem){
       if(arr.indexOf(elem) !=arr.lastIndexOf(elem) && result.indexOf(elem) == -1){
           result.push(elem);
       }
    });
    return result;
}
```

------

## 题目描述

为数组 arr 中的每个元素求二次方。不要直接修改数组 arr，结果返回新的数组

示例1

## 输入

```
[1, 2, 3, 4]
```

## 输出

```
[1, 4, 9, 16]
```

```
function square(arr) {
    var newArr = arr.slice();
    newArr.forEach(function(item,index){	//forEach()方法调用数组的每一个元素
        newArr[index] = newArr[index] * newArr[index];
    });
    return newArr;
}

// 使用map，map方法返回一个新数组，不修改原数组
  function square(arr) {
      return arr.map(function(e) {
          return e * e;
      })
  }
  // ES6箭头函数版
  const square = arr => arr.map(e => e * e);
```

------

## 题目描述

请修复给定的 js 代码中，函数定义存在的问题

示例1

## 输入

```
true
```

## 输出

```
a
```

```
//这里是需要修改的源代码
function functions(flag) {
    if (flag) {
      function getValue() { return 'a'; }
    } else {
      function getValue() { return 'b'; }
    }

    return getValue();
}
```

```
//上述源代码，两次声明了getValue（）函数，虽然不会赋值，但是声明了，也就是说返回的是重写的getValue函数
function functions(flag) {
    var getValue = function(){
        if(flag){
            return 'a';
        }else{
            return 'b';
        }
    }

    return getValue();
}
```

------

## 题目描述

修改 js 代码中 parseInt 的调用方式，使之通过全部测试用例

示例1

## 输入

```
'12'
```

## 输出

```
12
```

示例2

## 输入

```
'12px'
```

## 输出

```
12
```

示例3

## 输入

```
'0x12'
```

## 输出

```
0
```

```
function parse2Int(num) {
    return parseInt(num,10);
}
//parseInt(string, radix) 当参数 radix 的值为 0，或没有设置该参数时，parseInt() 会根据 string 来判断数字的基数。
//举例，如果 string 以 "0x" 开头，parseInt() 会把 string 的其余部分解析为十六进制的整数。如果 string 以 0 开头，那么 ECMAScript v3 允许 parseInt() 的一个实现把其后的字符解析为八进制或十六进制的数字。如果 string 以 1 ~ 9 的数字开头，parseInt() 将把它解析为十进制的整数。
```

------

## 题目描述

判断 val1 和 val2 是否完全等同

```
function identity(val1, val2) {
    return val1===val2?true:false;	//其实这么写复杂了，可以这样 return val1===val2
}


```

------

## 题目描述

实现一个打点计时器，要求
1、从 start 到 end（包含 start 和 end），每隔 100 毫秒 console.log 一个数字，每次数字增幅为 1
2、返回的对象中需要包含一个 cancel 方法，用于停止定时操作
3、第一个数需要立即输出

```

function count(start, end) {
  //立即输出第一个值
  console.log(start++);
     var timer = setInterval(function(){
         if(start <= end){
             console.log(start++);
         }else{
             clearInterval(timer);
         }
     },100);
    //返回一个对象
     return {
         cancel : function(){
             clearInterval(timer);
         }
     };
 }
```

------


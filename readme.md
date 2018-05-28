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

## 题目描述

实现 fizzBuzz 函数，参数 num 与返回值的关系如下：
1、如果 num 能同时被 3 和 5 整除，返回字符串 fizzbuzz
2、如果 num 能被 3 整除，返回字符串 fizz
3、如果 num 能被 5 整除，返回字符串 buzz
4、如果参数为空或者不是 Number 类型，返回 false
5、其余情况，返回参数 num

示例1

## 输入

```
15
```

## 输出

```
fizzbuzz
```

```
function fizzBuzz(num) {
    if(num%3==0 && num%5==0){
        return 'fizzbuzz';
    }else if(num%3==0){
        return 'fizz';
    }else if(num%5==0){
        return 'buzz';
    }else if(num==null || typeof num!= 'number'){
        return false;
    }else {
        return num;
    }
}

//为什么写num==null呢？其实写num==undefined也是可以的，会隐式转换，但是不可以写 !num, 
因为 !num 可以包括 0 undefined null false ''
```

------

## 题目描述

将数组 arr 中的元素作为调用函数 fn 的参数

示例1

## 输入

```
function (greeting, name, punctuation) {return greeting + ', ' + name + (punctuation || '!');}, ['Hello', 'Ellie', '!']
```

## 输出

```
Hello, Ellie!
```

```
function argsAsArray(fn, arr) {
  return fn.apply(this, arr);
 }
 
调用函数可以使用call或者apply这两个方法，区别在于call需要将传递给函数的参数明确写出来，是多少参数就需要写多少参数。而apply则将传递给函数的参数放入一个数组中，传入参数数组即可。
```

------

## 题目描述

将函数 fn 的执行上下文改为 obj 对象

示例1

## 输入

```
function () {return this.greeting + ', ' + this.name + '!!!';}, {greeting: 'Hello', name: 'Rebecca'}
```

## 输出

```
Hello, Rebecca!!!
```

```

在JavaScript中，函数是一种对象，其上下文是可以变化的，对应的，函数内的this也是可以变化的，函数可以作为一个对象的方法，也可以同时作为另一个对象的方法，可以通过Function对象中的call或者apply方法来修改函数的上下文，函数中的this指针将被替换为call或者apply的第一个参数。将函数 fn 的执行上下文改为 obj 对象，只需要将obj作为call或者apply的第一个参数传入即可。

function speak(fn, obj) {
  return fn.apply(obj, obj);
 }
```

------

## 题目描述

实现函数 functionFunction，调用之后满足如下条件：
1、返回值为一个函数 f
2、调用返回的函数 f，返回值为按照调用顺序的参数拼接，拼接字符为英文逗号加一个空格，即 ', '
3、所有函数的参数数量为 1，且均为 String 类型

示例1

## 输入

```
functionFunction('Hello')('world')
```

## 输出

```
Hello, world
```

```


function functionFunction(str) {
  var f = function(s){
         return str+", "+s;
     }
     return f;
 }
```

------

## 题目描述

实现函数 makeClosures，调用之后满足如下条件：
1、返回一个函数数组 result，长度与 arr 相同
2、运行 result 中第 i 个函数，即 result[i]()，结果与 fn(arr[i]) 相同

示例1

## 输入

```
[1, 2, 3], function (x) { 
	return x * x; 
}
```

## 输出

```
4
```

```


function makeClosures(arr, fn) {
  var result = [];
     arr.forEach(function(e){
         result.push(function(num){
             return function(){
                 return fn(num);
             };
         }(e));
     });
     return result;
 }
 

//使用ES6 let语法
function makeClosures(arr, fn) {   
    var result = new Array();
    for(let i=0;i<arr.length;i++){
        result[i] = function(){
            return fn(arr[i]); //let声明的变量只在let所在代码块内有效，因此每次循环的i都是一个新的变量           
        };
    }
    return result;
}

//使用ES5的bind()方法
function makeClosures(arr, fn) {
    var result = new Array();
    for(var i=0;i<arr.length;i++){
        result[i] = fn.bind(null,arr[i]);
    }
    return result;
}

```

------

## 题目描述

已知函数 fn 执行需要 3 个参数。请实现函数 partial，调用之后满足如下条件：
1、返回一个函数 result，该函数接受一个参数
2、执行 result(str3) ，返回的结果与 fn(str1, str2, str3) 一致

示例1

## 输入

复制

```
var sayIt = function(greeting, name, punctuation) {     return greeting + ', ' + name + (punctuation || '!'); };  partial(sayIt, 'Hello', 'Ellie')('!!!');
```

## 输出

复制

```
Hello, Ellie!!!
```

```


// call
function partial(fn, str1, str2) {
    function result(str3) {
        return fn.call(this, str1, str2, str3);
    }
 
     return result;
}
 
// apply（这里只是为了对照）
function partial(fn, str1, str2) {
    function result(str3) {
        return fn.apply(this, [str1, str2, str3]);
    }
 
    return result;
}
 
// 这个bind会生成一个新函数（对象）, 它的str1, str2参数都定死了, str3未传入, 一旦传入就会执行
function partial(fn, str1, str2) {
    return fn.bind(this, str1, str2); // 或 return fn.bind(null, str1, str2);
}
 
// bind同上, 多了一步, 把str3传入的过程写在另一个函数里面,
// 而另一个函数也有str1, str2参数
// 此法有种多次一举的感觉，但是表示出了后续的调用。
function partial(fn, str1, str2) {
    function result(str3) {
        return fn.bind(this, str1, str2)(str3);
    }
 
    return result;
}
 
// 匿名函数，默认this绑定global，与bind的第一个参数为this时效果一样。
function partial(fn, str1, str2) {
    return function(str3) {
        return fn(str1, str2, str3);
    }
}
 
// ES6。this指向undefined.
const partial = (fn, str1, str2) => str3 => fn(str1, str2, str3);
```

------

## 题目描述

函数 useArguments 可以接收 1 个及以上的参数。请实现函数 useArguments，返回所有调用参数相加后的结果。本题的测试参数全部为 Number 类型，不需考虑参数转换。

示例1

## 输入

复制

```
1, 2, 3, 4
```

## 输出

复制

```
10
```

```


本题考查的是对于arguments的使用，arguments能获得函数对象传入的参数组，类似与一个数组，能够通过length获取参数个数，能通过下标获取该位置的参数，但是它不能使用forEach等方法。本题先通过arguments.length获得参数个数，然后循环求和，得出结果。
function useArguments() {
    var sum = 0;
    for(var i=0;i<arguments.length;i++){
        sum+=arguments[i];
    };
    return sum;
}
```

------

## 题目描述

实现函数 callIt，调用之后满足如下条件
1、返回的结果为调用 fn 之后的结果
2、fn 的调用参数为 callIt 的第一个参数之后的全部参数

示例1

## 输入

复制

```
无
```

## 输出

复制

```
无
```

```

function callIt(fn) {
    //将arguments转化为数组后，截取第一个元素之后的所有元素
    var args = Array.prototype.slice.call(arguments,1);
    //调用fn
    var result = fn.apply(null,args);
    return result;
}



```

------

## 题目描述

实现函数 partialUsingArguments，调用之后满足如下条件：
1、返回一个函数 result
2、调用 result 之后，返回的结果与调用函数 fn 的结果一致
3、fn 的调用参数为 partialUsingArguments 的第一个参数之后的全部参数以及 result 的调用参数

示例1

## 输入

复制

```
无
```

## 输出

复制

```
无
```

```
function partialUsingArguments(fn) {
    var arg = Array.prototype.slice.call(arguments,1);
    var result = function(){
        return fn.apply(null,arg.concat([].slice.call(arguments)) )
    }
    return result;
}
```

------

## 题目描述

已知 fn 为一个预定义函数，实现函数 curryIt，调用之后满足如下条件：
1、返回一个函数 a，a 的 length 属性值为 1（即显式声明 a 接收一个参数）
2、调用 a 之后，返回一个函数 b, b 的 length 属性值为 1
3、调用 b 之后，返回一个函数 c, c 的 length 属性值为 1
4、调用 c 之后，返回的结果与调用 fn 的返回值一致
5、fn 的参数依次为函数 a, b, c 的调用参数

示例1

## 输入

复制

```
var fn = function (a, b, c) {return a + b + c}; curryIt(fn)(1)(2)(3);
```

## 输出

复制

```
6
```

```


柯里化是把接受多个参数的函数变换成接受一个单一参数(最初函数的第一个参数)的函数，并且返回接受余下的参数且返回结果的新函数的技术。简单理解题目意思，就是指，我们将预定义的函数的参数逐一传入到curryIt中，当参数全部传入之后，就执行预定义函数。于是，我们首先要获得预定义函数的参数个数fn.length，然后声明一个空数组去存放这些参数。返回一个匿名函数接收参数并执行，当参数个数小于fn.length，则再次返回该匿名函数，继续接收参数并执行，直至参数个数等于fn.length。最后，调用apply执行预定义函数。

function curryIt(fn) {
     //获取fn参数的数量
     var n = fn.length;
     //声明一个数组args
     var args = [];
     //返回一个匿名函数
     return function(arg){
         //将curryIt后面括号中的参数放入数组
         args.push(arg);
         //如果args中的参数个数小于fn函数的参数个数，
         //则执行arguments.callee（其作用是引用当前正在执行的函数，这里是返回的当前匿名函数）。
         //否则，返回fn的调用结果
         if(args.length < n){
            return arguments.callee;
         }else return fn.apply("",args);
     }
 }
```

------

## 题目描述

完成函数 createModule，调用之后满足如下要求：
1、返回一个对象
2、对象的 greeting 属性值等于 str1， name 属性值等于 str2
3、对象存在一个 sayIt 方法，该方法返回的字符串为 greeting属性值 + ', ' + name属性值

```
function createModule(str1, str2) {
    var obj = {
        greeting: str1,
        name: str2,
        sayIt: function(){
            return this.greeting+", "+this.name;
        }
    };
    return obj;
}
```

------

## 题目描述

获取数字 num 二进制形式第 bit 位的值。注意：
1、bit 从 1 开始
2、返回 0 或 1
3、举例：2 的二进制为 10，第 1 位为 0，第 2 位为 1

示例1

## 输入

复制

```
128, 8
```

## 输出

复制

```
1
```

```
function valueAtBit(num, bit) {
var len = num.toString(2);
    return len[len.length-bit]
}

```

------

## 题目描述

获取数字 num 二进制形式第 bit 位的值。注意：
1、bit 从 1 开始
2、返回 0 或 1
3、举例：2 的二进制为 10，第 1 位为 0，第 2 位为 1

示例1

## 输入

复制

```
128, 8
```

## 输出

复制

```
1
```

```
function valueAtBit(num, bit) {
  var s = num.toString(2);
     return s[s.length - bit];
 }

function valueAtBit(num, bit) {
    //toString转化为二进制，split将二进制转化为数组，reverse()将数组颠倒顺序
    var arr = num.toString(2).split("").reverse();
    return arr[bit-1];
}

//这个思路很新奇，我也看不懂
function valueAtBit(num, bit) {
    return (num >> (bit -1)) & 1;
}

```

------

## 题目描述

给定二进制字符串，将其换算成对应的十进制数字

示例1

## 输入

复制

```
'11000000'
```

## 输出

复制

```
192
```

```
parseInt方法的可选参数是操作数的进制说明，不是目标的进制。
数字转字符用toString()，字符转数字用parseInt() or parseFloat().
其它进制转十进制
        parseInt(str,2)
        parseInt(str,8)
        parseInt(str,16)
        
function base10(str) {
    return parseInt(str,2)
}
```

------

## 题目描述

将给定数字转换成二进制字符串。如果字符串长度不足 8 位，则在前面补 0 到满8位。

示例1

## 输入

复制

```
65
```

## 输出

复制

```
01000001
```

```
//只要长度没有达到8，就会在字符串前面一直加  0  
function convertToBinary(num) {
    var str = num.toString(2);
    while(str.length < 8) {
        str = "0" + str;
    }
     
    return str;
}

function convertToBinary(num) {
     //转换为2进制格式
     var s = num.toString(2);
     //获得2进制数长度
     var l = s.length;
     if(l<8){
         //声明一个字符串用于补满0
         var s1 = "0000000";
         var s2 = s1.slice(0,8-l);
         s = s2+s; 
     }
     return s;
 }
```

------

## 题目描述

求 a 和 b 相乘的值，a 和 b 可能是小数，需要注意结果的精度问题

示例1

## 输入

复制

```
3, 0.0001
```

## 输出

复制

```
0.0003
```

```
//精度应该为两个小数位数长度的和
function multiply(a, b) {
    var strA = ''+a;
    var strB = ''+b;
    var lenA = (strA.indexOf('.')==-1)?0:(strA.length-strA.indexOf('.')-1);
    var lenB = (strB.indexOf('.')==-1)?0:(strB.length-strB.indexOf('.')-1);
    var len = lenA+lenB
    var result = (a*b).toFixed(len);
    return result;
}
```

------

## 题目描述

将函数 fn 的执行上下文改为 obj，返回 fn 执行后的值

示例1

## 输入

复制

```
alterContext(function() {return this.greeting + ', ' + this.name + '!'; }, {name: 'Rebecca', greeting: 'Yo' })
```

## 输出

复制

```
Yo, Rebecca!
```

```


在JavaScript中，函数是一种对象，其上下文是可以变化的，对应的，函数内的this也是可以变化的，函数可以作为一个对象的方法，也可以同时作为另一个对象的方法，可以通过Function对象中的call或者apply方法来修改函数的上下文，函数中的this指针将被替换为call或者apply的第一个参数。将函数 fn 的执行上下文改为 obj 对象，只需要将obj作为call或者apply的第一个参数传入即可。

function alterContext(fn, obj) {
    return fn.call(obj)
}
```

------

## 题目描述

给定一个构造函数 constructor，请完成 alterObjects 方法，将 constructor 的所有实例的 greeting 属性指向给定的 greeting 变量。

示例1

## 输入

复制

```
var C = function(name) {this.name = name; return this;}; 
var obj1 = new C('Rebecca'); 
alterObjects(C, 'What\'s up'); obj1.greeting;
```

## 输出

复制

```
What's up
```

```

这是原型链问题。访问一个对象的方法或者是属性，首先会在该对象中寻找，如果找到则返回，如果没找到，则在其原型链上面向上寻找，直至基原型，如还未找到，则返回undefined。将 constructor 的所有实例的 greeting 属性指向给定的 greeting 变量，只需要在constructor的原型上面添加greeting属性，并指定值。

function alterObjects(constructor, greeting) {
  constructor.prototype.greeting = greeting;
 }
```

------

## 题目描述

找出对象 obj 不在原型链上的属性(注意这题测试例子的冒号后面也有一个空格~)
1、返回数组，格式为 key: value
2、结果数组不要求顺序

示例1

## 输入

复制

```
var C = function() {this.foo = 'bar'; this.baz = 'bim';}; 
C.prototype.bop = 'bip'; 
iterate(new C());
```

## 输出

复制

```
["foo: bar", "baz: bim"]
```

```


可以使用for-in来遍历对象中的属性，hasOwnproperty方法能返回一个布尔值，指出一个对象是否具有指定名称的属性。此方法无法检查该对象的原型链中是否具有该属性，该属性必须为对象本身的属性。
function iterate(obj) {
     var arr = [];
     //使用for-in遍历对象属性
     for(var key in obj){
         //判断key是否为对象本身的属性
         if(obj.hasOwnProperty(key)){
             //将属性和值按格式存入数组
             arr.push(key+": "+obj[key]);
         }
     }
     return arr;
 }
```

------

## 题目描述

给定字符串 str，检查其是否包含数字，包含返回 true，否则返回 false

示例1

## 输入

复制

```
'abc123'
```

## 输出

复制

```
true
```

```
function containsNumber(str) {
    var b = /\d/;
    return b.test(str)
}
```

------

## 题目描述

给定字符串 str，检查其是否包含连续重复的字母（a-zA-Z），包含返回 true，否则返回 false

示例1

## 输入

复制

```
'rattler'
```

## 输出

复制

```
true
```

```
在正则表达式中，利用()进行分组，使用斜杠加数字表示引用，\1就是引用第一个分组，\2就是引用第二个分组。将[a-zA-Z]做为一个分组，然后引用，就可以判断是否有连续重复的字母。

function containsRepeatingLetter(str) {
     return /([a-zA-Z])\1/.test(str);
 }
```

------

## 题目描述

给定字符串 str，检查其是否以元音字母结尾
1、元音字母包括 a，e，i，o，u，以及对应的大写
2、包含返回 true，否则返回 false

示例1

## 输入

复制

```
'gorilla'
```

## 输出

复制

```
true
```

```
首先确定元音集合[a,e,i,o,u]，然后是以元音结尾，加上$，最后通配大小写，加上i。因此正则表达式为:/[a,e,i,o,u]$/i，最后用test方法去检测字符串str

function endsWithVowel(str) {
  return /[a,e,i,o,u]$/i.test(str);
 }
```

------

## 题目描述

给定字符串 str，检查其是否包含 连续3个数字 
1、如果包含，返回最新出现的 3 个数字的字符串
2、如果不包含，返回 false

示例1

## 输入

复制

```
'9876543'
```

## 输出

复制

```
987
```

```
题目描述有问题，实际考察的是字符串中是否含有连续的三个任意数字，而不是三个连续的数字。依题，若存在连续的三个任意数字，则返回最早出现的三个数字，若不存在，则返回false。因此需要用到match方法，match()返回的是正则表达式匹配的字符串数组，连续的三个任意数字用正则表达式表示为/\d{3}/。

function captureThreeNumbers(str) {
     //声明一个数组保存匹配的字符串结果
  var arr = str.match(/\d{3}/);
     //如果arr存在目标结果，则返回第一个元素，即最早出现的目标结果
     if(arr)
         return arr[0];
     else return false;
 }
```

------

## 题目描述

给定字符串 str，检查其是否符合如下格式
1、XXX-XXX-XXXX
2、其中 X 为 Number 类型

示例1

## 输入

复制

```
'800-555-1212'
```

## 输出

复制

```
true
```

```
function matchesPattern(str) {
    return/^(\d{3}-){2}\d{4}$/.test(str);
}
```

------

## 题目描述

给定字符串 str，检查其是否符合美元书写格式
1、以 $ 开始
2、整数部分，从个位起，满 3 个数字用 , 分隔
3、如果为小数，则小数部分长度为 2
4、正确的格式如：$1,023,032.03 或者 $2.03，错误的格式如：$3,432,12.12 或者 $34,344.3

示例1

## 输入

复制

```
'$20,933,209.93'
```

## 输出

复制

```
true
```

```
function isUSD(str) {
    var re = /^\$([1-9]\d{0,2}(,\d{3})*|0)(\.\d{2})?$/;
    return re.test(str);
}
\$ 转义字符

```

------

```
链接：https://www.nowcoder.com/questionTerminal/667dd00250d04d06989ed1b69102c9ab
来源：牛客网

hefeng6500 整理
```


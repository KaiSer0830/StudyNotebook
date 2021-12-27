大文件排序用什么排序法



# JavaScript数组操作方法总结



![JS数组操作](D:/DeskTop/%E5%89%8D%E7%AB%AF%E4%B9%A6%E7%B1%8Dpdf%E6%95%99%E7%A8%8B/%E5%89%8D%E7%AB%AF%E9%9D%A2%E8%AF%95%E9%A2%98%E5%87%86%E5%A4%87/%E5%A4%A7%E5%8E%82%E5%89%8D%E7%AB%AF%E9%9D%A2%E8%AF%95%E8%B5%84%E6%96%99/%E7%AC%94%E8%AE%B0/JS%E6%95%B0%E7%BB%84%E6%93%8D%E4%BD%9C.png)

## 数组的遍历查找

### for循环

```
let arr = [1, 2, 3, 4, 5];
for (let i = 0; i < arr.length; i++) {
	console.log(arr[i]);
}
// 1
// 2
// 3
// 4
// 5
```

### for... of 循环

- `for...of `语句遍历可迭代对象定义要迭代的数据。简单来说，`for...of`遍历的就是value。

```
let arr = ['Chocolate', 'zhlll', 'lionkk'];
for (let val of arr) {
	console.log(val);
}
// Chocolate
// zhlll
// lionkk
```

### for... in 循环

- `for...in`语句以任意顺序迭代对象的**可枚举属性**。简单来说，`for...in`遍历的就是 key。对于数组，key对应着的是数组的**下标索引**。

```
let arr = ['Chocolate', 'zhlll', 'lionkk'];
for (let key in arr) {
	console.log(key);
}
// 0
// 1
// 2
```

### array.forEach()方法

语法：

```
array.forEach(function(currentValue, index, arr), thisValue)
```

| 参数         | 描述                                                         |
| :----------- | :----------------------------------------------------------- |
| currentValue | 必需。 当前元素                                              |
| index        | 可选。当前元素的索引值                                       |
| arr          | 可选。当前元素所属的数组对象。                               |
| *thisValue*  | 可选。传递给函数的值一般用 "this" 值。 如果这个参数为空， "undefined" 会传递给 "this" 值 |

```
let arr = ['Chocolate', 'zhlll', 'lionkk'];
arr.forEach(function (cur, index, arr) {
	console.log(cur, index, arr);
})
// Chocolate 0 [ 'Chocolate', 'zhlll', 'lionkk' ]
// zhlll 1 [ 'Chocolate', 'zhlll', 'lionkk' ]
// lionkk 2 [ 'Chocolate', 'zhlll', 'lionkk' ]
```

发现后面两个参数是可选的，那么可以让后两个参数按需添加即可：

```
let arr = ['Chocolate', 'zhlll', 'lionkk'];
arr.forEach((cur) => {
	console.log(cur);
})
// Chocolate
// zhlll
// lionkk
```

> **疑难点：thisValue**

```
function Foo() {
  this.sum = 0
  this.cnt = 0
}
// 在原型上添加一个名为 doSth 方法
Foo.prototype.doSth = function (arr) {
  arr.forEach(function (cur) {
    this.sum += cur
    this.cnt++
  }, this) // this 指向实例对象
}
let foo = new Foo()
let arr = [1, 2, 3]
foo.doSth(arr)
console.log(foo.sum, foo.cnt)
// 6 3
// 解释： 6 === (1+2+3) 3 === (1+1+1)
```

`注意：如果使用箭头函数表达式来传入函数参数， thisArg 参数会被忽略，因为箭头函数在词法上绑定了 this 值。`

因此，如果对于普通函数的话，可以看做是将 this 通过传参的形式解决无法继承 问题，当然，通过箭
头函数的方式是一个不错的选择！



### map遍历

- 返回一个新数组，其结果是该数组中的每个元素 是调用一次提供的回调函数后的返回值。

**语法：**

```
let newArray = array.map(function(currentValue, index, arr), thisArg)
```

| callback     | 为数组中每个元素执行的函数，该函数接收一至三个参数 |
| ------------ | -------------------------------------------------- |
| currentValue | 数组中正在处理的当前元素                           |
| index (可选) | 数组中正在处理的当前元素的索引                     |
| arr (可选)   | map() 方法正在操作的数组                           |
| thisArg      | 可选参数,当执行回调函数callback,用作this值         |

示例：

```
let arr = ['Chocolate', 'zhlll', 'lionkk'];
let newArr = arr.map(function (cur, index, arr) {
  console.log(cur, index, arr);
  return cur + index;
})
// Chocolate 0 [ 'Chocolate', 'zhlll', 'lionkk' ]
// zhlll 1 [ 'Chocolate', 'zhlll', 'lionkk' ]
// lionkk 2 [ 'Chocolate', 'zhlll', 'lionkk' ]
console.log(newArr)
// [ 'Chocolate0', 'zhlll1', 'lionkk2' ]
```

```
function Foo() {
  this.sum = 0;
  this.cnt = 0;
}
// 在原型上添加一个名为 doSth 方法
Foo.prototype.doSth = function (arr) {
  let newArr = arr.map(function (cur) {
    this.sum += cur;
    this.cnt++;
    return cur + 10;
  }, this) // this 指向实例对象
  return newArr;
}
let foo = new Foo();
let arr = [1, 2, 3];
console.log(foo.doSth(arr)); // [ 11, 12, 13 ]
console.log(foo.sum);// 6
console.log(foo.cnt);// 3
```

**一些技巧性操作**

```
let arr = [1, 4, 9, 16];
let res = arr.map(Math.sqrt); // 传入Math中sqrt得到数组中每个元素的平方根
console.log(res); // [ 1, 2, 3, 4 ]
```

> **总结：**

- map 不修改调用它的原数组本身（当然可以在 callback 执行时改变原数组）
  回调函数不返回值时，最后新数组的每个值都为undefined
- this 的值最终相对于 callback 函数的可观察性是依据this规则，也就是 this 指向问题
- map 会返回一个新数组



### reduce遍历

- 对数组中的每个元素执行一个由您提供的 reducer 函数(升序执行)，将其结果汇总为单个返回值。

**语法：**

```
let res= array.reduce(callback(accumulator, currentValue, currentIndex, array),
initialValue)
```

| callback     | 为数组中每个元素执行的函数，该函数接收一至4个参数            |
| ------------ | ------------------------------------------------------------ |
| accumulator  | 累计器                                                       |
| currentValue | 当前值                                                       |
| currentIndex | 当前索引                                                     |
| array        | 数组                                                         |
| initialValue | 作为第一次调用 callback函数时的第一个参数的值。 如果没有提供初始值，则将使用数组中的第一个元素。 在没有初始值的空数组上调用 reduce 将报错。 |

```
let arr = [3, 5, 7, 1, 2];
let res = arr.reduce(function (acc, cur, index, arr) {
  console.log(acc, cur, index, arr);
  return acc + cur;
}, 0)
// 0 3 0 [ 3, 5, 7, 1, 2 ]
// 3 5 1 [ 3, 5, 7, 1, 2 ]
// 8 7 2 [ 3, 5, 7, 1, 2 ]
// 15 1 3 [ 3, 5, 7, 1, 2 ]
// 16 2 4 [ 3, 5, 7, 1, 2 ]
console.log(res);
// 18
```

> 总结：

- 如果数组为空且没有提供 initialValue ，会抛出TypeError 。
- 如果没有提供 initialValue ， reduce 会从索引1的地方开始执行 callback 方法，跳过第一个
  索引。如果提供 initialValue ，从索引0开始。
- acc 为传入函数的返回值，如果是 console.log ，则返回默认值 undefined



**reduce的用法：**

##### 数组求和

```js
const arr = [12, 34, 23];
const sum = arr.reduce((total, num) => total + num);

// 设定初始值求和
const arr = [12, 34, 23];
const sum = arr.reduce((total, num) => total + num, 10);  // 以10为初始值求和


// 对象数组求和
var result = [
  { subject: 'math', score: 88 },
  { subject: 'chinese', score: 95 },
  { subject: 'english', score: 80 }
];
const sum = result.reduce((accumulator, cur) => accumulator + cur.score, 0); 
const sum = result.reduce((accumulator, cur) => accumulator + cur.score, -10);  // 总分扣除10分
```

##### 数组最大值

```js
const a = [23,123,342,12];
const max = a.reduce((pre,next)=>pre>cur?pre:cur,0); // 342
```

##### 数组转对象

```js
var streams = [{name: '技术', id: 1}, {name: '设计', id: 2}];
var obj = streams.reduce((accumulator, cur) => {accumulator[cur.id] = cur; return accumulator;}, {});
```

##### 扁平一个二维数组

```js
var arr = [[1, 2, 8], [3, 4, 9], [5, 6, 10]];
var res = arr.reduce((x, y) => x.concat(y), []);
```

##### 数组去重

```text
实现的基本原理如下：

① 初始化一个空数组
② 将需要去重处理的数组中的第1项在初始化数组中查找，如果找不到（空数组中肯定找不到），就将该项添加到初始化数组中
③ 将需要去重处理的数组中的第2项在初始化数组中查找，如果找不到，就将该项继续添加到初始化数组中
④ ……
⑤ 将需要去重处理的数组中的第n项在初始化数组中查找，如果找不到，就将该项继续添加到初始化数组中
⑥ 将这个初始化数组返回
var newArr = arr.reduce(function (prev, cur) {
    prev.indexOf(cur) === -1 && prev.push(cur);
    return prev;
},[]);
```

##### 对象数组去重

```js
const dedup = (data, getKey = () => { }) => {
    const dateMap = data.reduce((pre, cur) => {
        const key = getKey(cur)
        if (!pre[key]) {
            pre[key] = cur
        }
        return pre
    }, {})
    return Object.values(dateMap)
}
```

##### 求字符串中字母出现的次数

```js
const str = 'sfhjasfjgfasjuwqrqadqeiqsajsdaiwqdaklldflas-cmxzmnha';

const res = str.split('').reduce((pre,next)=>{
 pre[next] ? pre[next]++ : pre[next] = 1
 return pre 
},{})
```





### filter()

- 创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。

**语法：**

```
let newArray = array.filter(function(currentValue, index, arr), thisArg)
```

| callback     | 为数组中每个元素执行的函数，该函数接收一至三个参数 |
| ------------ | -------------------------------------------------- |
| currentValue | 数组中正在处理的当前元素                           |
| index(可选)  | 数组中正在处理的当前元素的索引                     |
| arr(可选)    | filter() 方法正在操作的数组                        |
| thisArg      | （可选参数）,当执行回调函数callback,用作this值     |

```
let arr = [1, 2, 3, 4, 5];
let newArr = arr.filter(function (cur, index) {
  console.log(cur, index);
  return cur % 2 == 0;
})
// 1 0
// 2 1
// 3 2
// 4 3
// 5 4
console.log(newArr); // [ 2, 4 ]
```

简单来说，就是`返回满足条件的结果`。

### every()

- 测试一个数组内的所有元素是否都能通过某个指定函数的测试，它返回的是一个 Boolean 类型的值。

**语法：**

```
array.every(function(currentValue, index, arr), thisArg)
```

| callback     | 为数组中每个元素执行的函数，该函数接收一至三个参数 |
| ------------ | -------------------------------------------------- |
| currentValue | 数组中正在处理的当前元素                           |
| index(可选)  | 数组中正在处理的当前元素的索引                     |
| arr(可选)    | filter() 方法正在操作的数组                        |
| thisArg      | （可选参数）,当执行回调函数callback,用作this值     |

```
let res1 = [1, 2, 3, 4, 5].every(function (cur) {
  return cur > 10;
})
console.log(res1); // false
let res2 = [1, 2, 3, 4, 5].every(function (cur) {
  return cur >= 1;
})
console.log(res2); // true
```

简单来说，就是返回`是否都能满足特定条件的结果`，用`布尔值`返回。



### some()

- 测试数组中是不是至少有1个元素通过了被提供的函数测试，它返回的是一个 Boolean类型的值

**语法：**

```
array.some(function(currentValue, index, arr), thisArg)
```

| callback     | 为数组中每个元素执行的函数，该函数接收一至三个参数 |
| ------------ | -------------------------------------------------- |
| currentValue | 数组中正在处理的当前元素                           |
| index(可选)  | 数组中正在处理的当前元素的索引                     |
| arr(可选)    | filter() 方法正在操作的数组                        |
| thisArg      | （可选参数）,当执行回调函数callback,用作this值     |

```
let res1 = [1, 2, 3, 4, 5].some(function (cur) {
  return cur > 10;
})
console.log(res1); // false
let res2 = [1, 2, 3, 4, 5].some(function (cur) {
  return cur === 1;
})
console.log(res2); // true
```

简单来说，就是返回`是否至少有1个满足特定条件的结果`，用`布尔值`返回。



### find 与 findIndex

- find: 返回数组中满足提供的测试函数的第一个元素的值。否则返回 undefined。
- findIndex：数组中通过提供测试函数的第一个元素的索引。否则，返回 -1。

```
let ele = array.find(function(elemnet, index, arr), thisArg)

let eleIndex = array.findIndex(function(elemnet, index, arr), thisArg)
```

| callback     | 为数组中每个元素执行的函数，该函数接收一至三个参数 |
| ------------ | -------------------------------------------------- |
| currentValue | 数组中正在处理的当前元素                           |
| index(可选)  | 数组中正在处理的当前元素的索引                     |
| arr(可选)    | filter() 方法正在操作的数组                        |
| thisArg      | （可选参数），当执行回调函数callback，用作this值   |

```
let res1 = [1, 2, 3, 4, 5].find(function (cur) {
  return cur > 2;
})
console.log(res1); // 3
let res2 = [1, 2, 3, 4, 5].findIndex(function (cur) {
  return cur > 2;
})
console.log(res2); // 2
```



### keys 与 entries

- keys() 方法返回一个包含数组中每个索引键的Array Iterator 对象。
- entries() 方法返回一个新的 Array Iterator对 象，该对象包含数组中每个索引的键/值对。

```
let arr = ['Chocolate', 'zhlll', 'lionkk'];
let itKeys = arr.keys();
let itEntries = arr.entries();
for (let it of itKeys) {
console.log(it);
}
// 0
// 1
// 2
for (let it of itEntries) {
console.log(it);
}
// [ 0, 'Chocolate' ]
// [ 1, 'zhlll' ]
// [ 2, 'lionkk' ]
```



### values() 与 valueof()

- values()方法返回一个新的 Array Iterator对 象，该对象包含数组每个索引的值
- valueOf() 方法可返回 Boolean 对象的原始值。

```
let itVals = arr.values();
for (let it of itVals) {
console.log(it);
}
// Chocolate
// zhlll
// lionkk

var fruits = ["Banana", "Orange", "Apple", "Mango"];
var v = fruits.valueOf();
// Banana,Orange,Apple,Mango
```



### Indexof() 与 lastIndexOf()

- indexOf() 方法可返回某个指定的字符串值在字符串中首次出现的位置，没有找到返回 -1。
- lastIndexOf() 方法可返回一个指定的字符串值最后出现的位置，如果指定第二个参数 start，则在一个字符串中的指定位置从后向前搜索。

```
var str="Hello world, welcome to the universe.";
var n=str.indexOf("welcome"); // 13

var str="I am from runoob，welcome to runoob site.";
var n=str.lastIndexOf("runoob"); // 28
```



### includes()

- includes() 方法用于判断字符串是否包含指定的子字符串。找到返回true

```
var str = "Hello world, welcome to the Runoob。";
var n = str.includes("world");   // true
```



## 改变原始数组方法

### sort()

- ```
  语法：arr.sort([compareFunction])
  ```

- > - compareFunction 可选，用来指定按某种顺序进行排列的函数。
  > - 如果省略，元素按照转换为的字符串的各个字符的Unicode位点进行排序。
  > - 否则，如果指明了compareFunction：
  > - 如果 compareFunction(a, b) 小于 0 ，那么 a会被排列到 b 之前；
  > - 如果 compareFunction(a, b) 等于 0 ， a 和b 的相对位置不变。
  > - 如果 compareFunction(a, b) 大于 0 ， b 会被排列到 a 之前

```
let arr = [1, 10, 2, 5, 8, 3];

arr.sort(); // 默认
console.log(arr); // [ 1, 10, 2, 3, 5, 8 ]

arr.sort((a, b) => a - b); // 从小到大排序
console.log(arr); // [ 1, 2, 3, 5, 8, 10 ]

arr.sort((a, b) => b - a); // 从大到小排序
console.log(arr); // [ 10, 8, 5, 3, 2, 1 ]
```



### push()

- 类似栈、队列的一些操作
- push()成功之后会返回数组的长度。

```
let arr = [1,2];
let res = arr.push(100);
console.log(arr); // [ 1, 2, 100 ]
console.log(res); // 3
```



### pop()

- 类似栈、队列的一些操作

```
let arr = [1, 2, 100];
let res = arr.pop();
console.log(arr); // [ 1, 2 ]
console.log(res); // 100
```



### shift()

- 类似栈、队列的一些操作

```
let arr = [1, 2, 100];
let res = arr.shift();
console.log(arr); // [ 2, 100 ]
console.log(res); // 1
```



### unshift()

- 定义：将一个或多个元素添加到数组的开头，并 (该方法修改原有数组)
- 注意：该方法会返回该数组的新长度

```
let arr = [1, 2, 100];
let res = arr.unshift(4, 5, 6);
console.log(arr); // [ 4, 5, 6, 1, 2, 100 ]
console.log(res); // 6
```



### reverse()

- 定义：将数组中元素的位置颠倒，并返回该数组。

```
let arr = [1, 2, 3];
arr.reverse();
console.log(arr);// [ 3, 2, 1 ]
```



### splice()

- 通过**`删除或替换`**现有元素或者原地添加新的元素来修改数组,并以数组形式返回被修改的内容。

- ```
  array.splice(start[, deleteCount[, item1[, item2[, ...]]]])
  ```

> - **start:** 指定修改的开始位置（从0计数）
> - 1. 如果超出了数组的长度，则从数组末尾开始添加内容
> - 2. 如果是负值，则表示从数组末位开始的第几位（从-1计数，这意味着-n是倒数第n个元素，并且等价于array.length-n）
> - 3. 如果负数的绝对值大于数组的长度，则表示开始位置为第0位deleteCount(可选) : 整数,表示要移除的数组元素个数
>

> - **deleteCount(可选)** : 整数,表示要移除的数组元素个数
> - 1. 如果 deleteCount 大于 start 之后的元素的总数，则从 start 后面的元素都将被 删除(含第start 位)
> - 2. 如果 deleteCount 被省略了，或者它的值大于等于array.length - start(也就是 说，如果它大于或者等于start之后的所有元素的数量)，那么start之后数组的所有元素都会被删除。
> - 3. 如果 deleteCount 是 0 或者负数，则不移除元素。这种情况下，至少应添加一个新 元素。item1, item2, …(可选)要添加进数组的元素,从start 位置开始。如果不指定，则 splice() 将只删除数组元素

> `item1, item2, *...*` 可选
>
> 要添加进数组的元素,从`start` 位置开始。如果不指定，则 `splice()` 将只删除数组元素。

```
// 从第2位开始插入“Chocolate”
let arr = ['one', 'two', 'three'];

arr.splice(2, 0, 'Chocolate');
console.log(arr);// [ 'one', 'two', 'Chocolate', 'three' ]
```



```
// 从第 2 位开始删除 1 个元素，然后插入“Chocolate”
let arr = ['one', 'two', 'three'];

arr.splice(2, 1, 'Chocolate');
console.log(arr);// [ 'one', 'two', 'Chocolate' ]
```



### fill()

- fill() 方法用于将一个固定值替换数组的元素。
- 语法：array.fill(value, start, end)

```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.fill("Runoob");  // Runoob,Runoob,Runoob,Runoob
```



## 数组的映射

### Array.map() 方法

- map() 方法返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值。
- map() 方法按照原始数组元素顺序依次处理元素。
- 注意： map() 不会对空数组进行检测。
- 注意： map() 不会改变原始数组。



### Array.from() 方法

- 定义：通过在每个数组项上使用 callback 调用结果来创建一个新数组。

**语法：**

```
Array.from(Array,callback(currentValue, index, arr))
```

```
let arr = [1, 2, 3];
let newArr = Array.from(arr, function (cur) {
	return cur + 10;
})
console.log(newArr);// [ 11, 12, 13 ]
```



## 数组的连接

### Array.concat() 方法

- `array.concat(array1[, array2, ...]) `将一个或多个数组连接到原始数组。
- `concat()` 方法用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。

```
let arrA = [1, 2, 3];
let arrB = [4, 5, 6];
let ans = arrA.concat(arrB);
console.log(ans);// [ 1, 2, 3, 4, 5, 6 ]
```



### ...展开修饰符

```
let arrA = [1, 2, 3];
let arrB = [4, 5, 6];
let ans = [...arrA, ...arrB];
console.log(ans);// [ 1, 2, 3, 4, 5, 6 ]
```



## 获取数组的片段

### Array.slice() 方法

- 返回一个新的数组对象，这一对象是一个由begin 和 end 决定的原数组的**`浅拷贝`**（包括begin，不包括 end）——原始数组不会被改变。

**语法：**

```
arr.slice([begin[, end]])
```

- **begin (可选)**
- 1  提取起始处的索引（从 0 开始），从该索引开始提取原数组元素。
- 2  如果该参数为负数，则表示从原数组中的倒数第几个元素开始提取
- 3  slice(-2) 表示提取原数组中的倒数第二个元素到最后一个元素（包含最后一个元素）
- 4  如果省略 begin，则 slice 从索引 0 开始。
- 5  如果 begin 大于原数组的长度，则会返回空数组。
- **end (可选)**
- 1  slice(1,4) 会提取原数组中从第二个元素开始一直到第四个元素的所有元素 （索引为 1, 2, 3的元素）
- 2  如果该参数为负数， 则它表示在原数组中的倒数第几个元素结束抽取。
- 3  如果 end 被省略，则 slice 会一直提取到原数组末尾。
- 4  如果 end 大于数组的长度，slice 也会一直提取到原数组末尾。

```
let fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango'];
let res = fruits.slice(1, 3);
let res1 = fruits.slice(1);
let res2 = fruits.slice(-1);
let res3 = fruits.slice(0, -1);
console.log(res); // [ 'Orange', 'Lemon' ]
console.log(res1);// [ 'Orange', 'Lemon', 'Apple', 'Mango' ]
console.log(res2);// [ 'Mango' ]
console.log(res3);// [ 'Banana', 'Orange', 'Lemon', 'Apple' ]
```



## 转换数组

### join()

- 定义：将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。如果数组只有一个项目，那么将返回该项目而不使用分隔符。

**语法：**

```
arr.join(separator)
```

```
let arr = ['one', 'two', 'three'];
let res = arr.join('^');
let res1 = arr.join('&');

console.log(res); // one^two^three
console.log(res1); // one&two&three
```



### split()

- 使用指定的分隔符字符串将一个 String 对象分割成子字符串数组，以一个指定的分割字串来决定每个拆分的位置。

**语法：**

```
str.split([separator[, limit]])
```

```
const str = 'The best Chocolate';

const words = str.split(' ');
console.log(words); // [ 'The', 'best', 'Chocolate' ]
console.log(words[2]); // Chocolate
```



### toString()

- 返回一个字符串，表示指定的数组及其元素。
- 当一个数组被作为文本值或者进行字符串连接操作时，将会自动调用其 toString 方法。

**语法：**

```
arr.toString()
```

```
let arr = ['one', 'two', 'three'];
console.log(arr.toString()); // one,two,three
```



## 数组的扁平化

### flat()

- 按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新数组返回。

**语法：**

```
var newArray = arr.flat([depth])
```

​		参数depth可选：指定要提取嵌套数组的结构深度，默认值为1.

​		返回值：一个包含将数组和子数组所有元素的新数组

```
const arr1 = [0, 1, 2, [3, 4]];
console.log(arr1.flat()); // [ 0, 1, 2, 3, 4 ]
const arr2 = [0, 1, 2, [[[3, 4]]]];
console.log(arr2.flat(2)); // [ 0, 1, 2, [ 3, 4 ] ]
```



## 总结备忘

- #### 添加/删除元素

  - `push(...items)`    --- 从结尾添加元素
  - `pop()`                  --- 从结尾提取元素
  - `shift()`                  --- 从开头提取元素
  - `unshift(...items)`  --- 从开头添加元素
  - `splice(pos, deleteCount, ...items)` - -从index开始:删除deleteCount 元素并在当前位置I插入元素
  - `slice(start, end)` 一它从所有元素的开始索引"start" 复制到"end" (不包括"end" )返回-一个新的数组。
  - `concat(...items)`一返回-个新数组:复制当前数组的所有成员并向其中添加items. 如果有任何items是一个数组，那么就取其元素。

- #### 查询元素

  - `index0f/lastIndex0f(item, pos)` - -从`pos`找到`item`,则返回索引否则返回`-1`.
  - `includes(value)`一如果数组有value, 则返回true，否则返回false。
  - `find/filter(func)` -通过函数过滤元素，返回true 条件的符合find函数的第一个值或符合 filter 函数的全部值。
  - `findIndex`和find 类似，但返回索引而不是值。

- #### 转换数组

  - `map(func)` 一从每个元素调用func 的结果创建一 个新数组。
  - `sort(func)` -将数组倒序排列，然后返回.
  - `reverse()` -在原地颠倒数组，然后返回它。
  - `split/join`一将字符串转换为数组并返回。
  - `reduce(func, initial)` - -通过为每个元素调用func 计算数组上的单个值并在调用之间传递中间结果。

- #### 迭代元素

  - `forEach(func)`一为每个元表调用 func ,不返回任何东西。

- #### 其他

  - `Array. isArray(arr)` 检查arr是否是一个数组。

- **请注意**，`sort, reverse 和splice` 方法修改数组本身。

- `arr.some(n)/arr.every(fn)`检查数组。

  - 在类似于map的数组的每个元素上调用函数fn.如果任何/所有结果`true`, 则返回`true `，否则返回`false`。

- `arr.fill(value, start, end)`一 从start 到end用value重填充数组。

- `arr.copyWithin(target, start, end)`一将其元素从`start` 到`end`在`target `位置复制到本身(覆盖现有) .















# JavaScript字符串操作方法总结

### charAt( )

参数为一个下标，默认为0，查询字符串对应下标的字符，超出范围返回空字符串

	var str='abcd'
	console.log( str.charAt() )	     // 'a'
	console.log( str.charAt(2) )     // 'c'
	console.log( str.charAt(100) )     // ''


### charCodeAt( )

参数为一个下标，默认为0，查询字符串对应下标的字符的Unicode编码，超出范围返回NaN

	var str='abcd'
	console.log( str.charCodeAt() )	     // 97
	console.log( str.charCodeAt(2) )	     // 99


### concat( )

链接字符串，相当于字符串相加。

	var str1='hello'
	var str2=' world'
	var str3=str1.concat(str2)	//相当于 var str3=str1+str2
	console.log(str3)	//'hello world'


### indexOf( )

检索字符串在被检索字符串中所在的开始位置（区分大小写），空字符串返回0，不传参数返回-1，不存在返回-1。

	var str='hello world'
	str.indexOf('')		//0
	str.indexOf('llo')		//2
	str.indexOf('World')		//-1


### match( )

match() 方法可在字符串内检索指定的值，或找到一个或多个正则表达式的匹配项组成的数组。

	var str='1 hello 2 world 3'
	str.match(/\d+/g)		//['1','2','3']


### replace( )

用于把字符串中的特定字符串替换成新的字符串，或者把符合正则表达式的字符串替换成新的字符串，返回替换后的字符串，第一个参数为被替换的字符串或表达式，第二个为插入的字符串。

	var str='1hello2world3'
	str.replace('h','H')		//1Hello2world3
	str.replace(/\d+/g,'0')		//0hello0word0
	str	//'1hello2world3'


### search( )

用于检索字符串中指定的子字符串开始的位置，或检索与正则表达式相匹配的子字符串所在的位置。如果没有找到则返回-1,用法与indexOf相似。

	var str='helloWorld'
	str.search('W')		//5
	str.search(/llo/)	//2


### slice( )

提取字符串片段，返回被提取的字符串。第一个参数为开始位置，必填，第二个参数为结束位置(不包括)，不填默认截取到最后。参数可以为负值，负值代表从后往前数

	var str='helloWorld'
	str.slice(1)	//'elloWorld'
	str.slice(0,4)		//'hell'


### split( )

用于分割字符串，返回分割后的片段组成的数组，第一个参数为分割标识符，第二个参数可选，表示分割后形成的数组保留的长度，不填默认保留全部

	var str='helloWorld'
	str.split('o')		//['hell','W','rld']
	str.split('',3)		//['h','e','l']


### toLowerCase( )

把字符串转化为小写。

	var str='abcdEFG'
	str.toLowerCase()	//'abcdefg'
	str			//’abcdEFG' 


### toUpperCase( )

把字符串转化为大写

	var str='abcdEFG'
	str.toUpperCase()	//'ABCDEFG'
	str			//’abcdEFG' 


### substr( )

提取字符串片段，返回被提取的字符串，第一个参数为开始位置，第二个参数为总共截取的长度，默认截取到原字符串的最后一位

	var str='abcdefg'
	str.substr(2,2)		//'cd'


### substring( )

提取字符串片段，返回被提取的字符串，第一个参数为开始位置，第二个参数为结束位置（不包括）,与slice( )类似。

	var str='abcdefg'
	str.sunstring(2,5)		//'cde'


## ES6新增操作方法

### for of

for of 方法用来遍历字符串。

	var str='abcd'
	for (let item of str){
		console.log(item)	
		//	'a'
		//	'b'
		//	'c'
		//	'd'
	}


### includes( )

判断字符串中是否存在某一个片段，返回布尔值。第二个参数为开始搜索的位置。

	var str='abcdefg'
	str.includse('cde')		//true


### Indexof() 与 lastIndexOf()

- indexOf() 方法可返回某个指定的字符串值在字符串中首次出现的位置，没有找到返回 -1。
- lastIndexOf() 方法可返回一个指定的字符串值最后出现的位置，如果指定第二个参数 start，则在一个字符串中的指定位置从后向前搜索。

```
var str="Hello world, welcome to the universe.";
var n=str.indexOf("welcome"); // 13

var str="I am from runoob，welcome to runoob site.";
var n=str.lastIndexOf("runoob"); // 28
```



### startsWith( )

判断字符串是否以传入的字符串为开始。第二个参数为开始搜索的位置。

	var str='helloWorld!'
	str.startWith('hello')		//true


### endsWith( )

判断字符串是否以传入的字符串为结尾。第二个参数为开始搜索的位置。

	var str='helloWorld!'
	str.endsWith('!')		//true


### repeat( )

将原字符串重复n次，返回新的字符串，传入小数会被取整Math.floor( )

	var str='a'
	str.repeat(3)		//'aaa'
	str.repeat(3.9)		//'aaa'


### padStart( )和padEnd( )

用于补全字符串到指定长度，第一个参数为目标长度，如果小于或等于原字符串长度则返回原字符串，第二个参数为补全的内容(长度不够补全会重复此字符串，长度超出需要的长度会被截取)，不写默认为空格，padStart( )从开始位置填充，padEnd( )从结束位置填充。

	var str='abc'
	str.padStart(5,'h')		//'hhabc'
	str.padStart(10,'hello')	//'hellohelabc'
	str.padEnd(5,'hello')	//'abche'
	str.padstart(5)		//'  abc'


### match和matchAll( )

**`match()`** 方法检索返回一个字符串匹配正则表达式的结果。

**`matchAll()`** 方法返回一个包含所有匹配正则表达式的结果及分组捕获组的迭代器。返回一个正则表达式在当前字符串的所有匹配。

#### 模板字符串

用反引号 ` 标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。

模板字符串中使用变量用${ }包括起来,大括号内部可以放入任意的 JavaScript 表达式，可以进行运算，以及引用对象属性。

```
	var username='xiaohei'
	`username=${username}`		//'username=xiaohei'
```

- 
  如果在模板字符串中需要使用反引号，则前面要用反斜杠转义。

```
	var username='xiaohei'
	`/`user/`name=${username}`		//'`user`name=xiaohei'
```

- 
  使用模板字符串表示多行字符串，所有的空格和缩进都会被保留在输出之中。

```
	$('#box').html(
		`
			<ul>
  				<li>first</li>
  				<li>second</li>
			</ul>
		`
	)
	//上面代码中，所有模板字符串的空格和换行，都是被保留的
	//如果不想要这个换行，可以使用trim方法消除它。
	$('#box').html(
		`
			<ul>
  				<li>first</li>
  				<li>second</li>
			</ul>
		`.trim()
	)
```

​	

### trim和trimEnd()和trimStart()

**`trim()`** 方法会从一个字符串的两端删除空白字符。在这个上下文中的空白字符是所有的空白字符 (space, tab, no-break space 等) 以及所有行终止符字符（如 LF，CR等）。

**[返回值]**  一个代表调用字符串两端去掉空白的新字符串。

**`trimEnd() `**方法从一个字符串的末端移除空白字符。trimRight() 是这个方法的别名。

**`trimStart()`** 方法从字符串的开头删除空格。`trimLeft()` 是此方法的别名。









## 正则表达式及自带属性

在js中定义正则表达式很简单，有两种方式，一种是**通过构造函数**，一种是**通过//**，也就是`两个斜杠`

​		使用构造函数定义正则表达式，注意大小写，否则就会不起作用。由于构造函数的参数是一个字符串，也可以是两个斜杠的方式定义，遇到一些特殊字符就需要使用\进行转义，**通过双斜杠的方式**定义同样的正则表达式

### RegExp.prototype.test()

`test()` 方法执行一个检索，用来查看正则表达式与指定的字符串是否匹配。返回 `true` 或 `false`。



### RegExp.prototype.exec()

`exec() `方法在一个指定字符串中执行一个搜索匹配。返回一个结果数组或 [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null)。

```
var re = /quick\s(brown).+?(jumps)/ig;
var result = re.exec('The Quick Brown Fox Jumps Over The Lazy Dog');
// 所以一般是   re.exec('xx')[1]
```

|          | 属性/索引        | 描述                                      | 例子                                          |
| -------- | ---------------- | ----------------------------------------- | --------------------------------------------- |
| `result` | `[0]`            | 匹配的全部字符串                          | `Quick Brown Fox Jumps`                       |
|          | `[1], ...[*n* ]` | 括号中的分组捕获                          | `[1] = Brown[2] = Jumps`                      |
|          | `index`          | 匹配到的字符位于原始字符串的基于0的索引值 | `4`                                           |
|          | `input`          | 原始字符串                                | `The Quick Brown Fox Jumps Over The Lazy Dog` |





### 正则表达式语法大全

#### 普通字符

| 字符   | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| [ABC]  | 匹配 **[...]** 中的所有字符，例如 **[aeiou]** 匹配字符串 "google runoob taobao" 中所有的 e o u a 字母。 |
| [^ABC] | 匹配除了 **[...]** 中字符的所有字符，例如 **[^aeiou]** 匹配字符串 "google runoob taobao" 中除了 e o u a 字母的所有字母。 |
| [A-Z]  | [A-Z] 表示一个区间，匹配所有大写字母，[a-z] 表示所有小写字母。 |
| [\s\S] | 匹配所有。\s 是匹配所有空白符，包括换行，\S 非空白符，不包括换行。 |
| \w     | 匹配字母、数字、下划线。等价于 [A-Za-z0-9_]                  |



#### 非打印字符

| 字符 | 描述                                                         |
| :--- | ------------------------------------------------------------ |
| \cx  | 匹配由x指明的控制字符。例如， \cM 匹配一个 Control-M 或回车符。x 的值必须为 A-Z 或 a-z 之一。否则，将 c 视为一个原义的 'c' 字符。 |
| \f   | 匹配一个换页符。等价于 \x0c 和 \cL。                         |
| \n   | 匹配一个换行符。等价于 \x0a 和 \cJ。                         |
| \r   | 匹配一个回车符。等价于 \x0d 和 \cM。                         |
| \s   | 匹配任何空白字符，包括空格、制表符、换页符等等。等价于 [ \f\n\r\t\v]。注意 Unicode 正则表达式会匹配全角空格符。 |
| \S   | 匹配任何非空白字符。等价于 [^ \f\n\r\t\v]。                  |
| \t   | 匹配一个制表符。等价于 \x09 和 \cI。                         |
| \v   | 匹配一个垂直制表符。等价于 \x0b 和 \cK。                     |



#### 特殊字符

| 特别字符 | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| $        | 匹配输入字符串的结尾位置。如果设置了 RegExp 对象的 Multiline 属性，则 $ 也匹配 '\n' 或 '\r'。要匹配 $ 字符本身，请使用 \$。 |
| ( )      | 标记一个子表达式的开始和结束位置。子表达式可以获取供以后使用。要匹配这些字符，请使用 \( 和 \)。 |
| *        | 匹配前面的子表达式零次或多次。要匹配 * 字符，请使用 \*。     |
| +        | 匹配前面的子表达式一次或多次。要匹配 + 字符，请使用 \+。     |
| .        | 匹配除换行符 \n 之外的任何单字符。要匹配 . ，请使用 \. 。    |
| [        | 标记一个中括号表达式的开始。要匹配 [，请使用 \[。            |
| ?        | 匹配前面的子表达式零次或一次，或指明一个非贪婪限定符。要匹配 ? 字符，请使用 \?。 |
| \        | 将下一个字符标记为或特殊字符、或原义字符、或向后引用、或八进制转义符。例如， 'n' 匹配字符 'n'。'\n' 匹配换行符。序列 '\\' 匹配 "\"，而 '\(' 则匹配 "("。 |
| ^        | 匹配输入字符串的开始位置，除非在方括号表达式中使用，当该符号在方括号表达式中使用时，表示不接受该方括号表达式中的字符集合。要匹配 ^ 字符本身，请使用 \^。 |
| {        | 标记限定符表达式的开始。要匹配 {，请使用 \{。                |
| \|       | 指明两项之间的一个选择。要匹配 \|，请使用 \|。               |



#### 限定符

| 字符  | 描述                                                         |
| ----- | ------------------------------------------------------------ |
| *     | 匹配前面的子表达式零次或多次。例如，zo* 能匹配 "z" 以及 "zoo"。* 等价于{0,}。 |
| +     | 匹配前面的子表达式一次或多次。例如，'zo+' 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。+ 等价于 {1,}。 |
| ?     | 匹配前面的子表达式零次或一次。例如，"do(es)?" 可以匹配 "do" 、 "does" 中的 "does" 、 "doxy" 中的 "do" 。? 等价于 {0,1}。 |
| {n}   | n 是一个非负整数。匹配确定的 n 次。例如，'o{2}' 不能匹配 "Bob" 中的 'o'，但是能匹配 "food" 中的两个 o。 |
| {n,}  | n 是一个非负整数。至少匹配n 次。例如，'o{2,}' 不能匹配 "Bob" 中的 'o'，但能匹配 "foooood" 中的所有 o。'o{1,}' 等价于 'o+'。'o{0,}' 则等价于 'o*'。 |
| {n,m} | m 和 n 均为非负整数，其中n <= m。最少匹配 n 次且最多匹配 m 次。例如，"o{1,3}" 将匹配 "fooooood" 中的前三个 o。'o{0,1}' 等价于 'o?'。请注意在逗号和两个数之间不能有空格。 |



#### 定位符

| 字符 | 描述                                                         |
| ---- | ------------------------------------------------------------ |
| ^    | 匹配输入字符串开始的位置。如果设置了 RegExp 对象的 Multiline 属性，^ 还会与 \n 或 \r 之后的位置匹配。 |
| $    | 匹配输入字符串结尾的位置。如果设置了 RegExp 对象的 Multiline 属性，$ 还会与 \n 或 \r 之前的位置匹配。 |
| \b   | 匹配一个单词边界，即字与空格间的位置。                       |
| \B   | 非单词边界匹配。                                             |



#### 元字符整合（包含所有）

| 字符         | 描述                                                         |
| :----------- | :----------------------------------------------------------- |
| \            | 将下一个字符标记为一个特殊字符、或一个原义字符、或一个 向后引用、或一个八进制转义符。例如，'n' 匹配字符 "n"。'\n' 匹配一个换行符。序列 '\\' 匹配 "\" 而 "\(" 则匹配 "("。 |
| ^            | 匹配输入字符串的开始位置。如果设置了 RegExp 对象的 Multiline 属性，^ 也匹配 '\n' 或 '\r' 之后的位置。 |
| $            | 匹配输入字符串的结束位置。如果设置了RegExp 对象的 Multiline 属性，$ 也匹配 '\n' 或 '\r' 之前的位置。 |
| *            | 匹配前面的子表达式零次或多次。例如，zo* 能匹配 "z" 以及 "zoo"。* 等价于{0,}。 |
| +            | 匹配前面的子表达式一次或多次。例如，'zo+' 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。+ 等价于 {1,}。 |
| ?            | 匹配前面的子表达式零次或一次。例如，"do(es)?" 可以匹配 "do" 或 "does" 。? 等价于 {0,1}。 |
| {n}          | n 是一个非负整数。匹配确定的 n 次。例如，'o{2}' 不能匹配 "Bob" 中的 'o'，但是能匹配 "food" 中的两个 o。 |
| {n,}         | n 是一个非负整数。至少匹配n 次。例如，'o{2,}' 不能匹配 "Bob" 中的 'o'，但能匹配 "foooood" 中的所有 o。'o{1,}' 等价于 'o+'。'o{0,}' 则等价于 'o*'。 |
| {n,m}        | m 和 n 均为非负整数，其中n <= m。最少匹配 n 次且最多匹配 m 次。例如，"o{1,3}" 将匹配 "fooooood" 中的前三个 o。'o{0,1}' 等价于 'o?'。请注意在逗号和两个数之间不能有空格。 |
| ?            | 当该字符紧跟在任何一个其他限制符 (*, +, ?, {n}, {n,}, {n,m}) 后面时，匹配模式是非贪婪的。非贪婪模式尽可能少的匹配所搜索的字符串，而默认的贪婪模式则尽可能多的匹配所搜索的字符串。例如，对于字符串 "oooo"，'o+?' 将匹配单个 "o"，而 'o+' 将匹配所有 'o'。 |
| .            | 匹配除换行符（\n、\r）之外的任何单个字符。要匹配包括 '\n' 在内的任何字符，请使用像"**(.\|\n)**"的模式。 |
| (pattern)    | 匹配 pattern 并获取这一匹配。所获取的匹配可以从产生的 Matches 集合得到，在VBScript 中使用 SubMatches 集合，在JScript 中则使用 $0…$9 属性。要匹配圆括号字符，请使用 '\(' 或 '\)'。 |
| (?:pattern)  | 匹配 pattern 但不获取匹配结果，也就是说这是一个非获取匹配，不进行存储供以后使用。这在使用 "或" 字符 (\|) 来组合一个模式的各个部分是很有用。例如， 'industr(?:y\|ies) 就是一个比 'industry\|industries' 更简略的表达式。 |
| (?=pattern)  | 正向肯定预查（look ahead positive assert），在任何匹配pattern的字符串开始处匹配查找字符串。这是一个非获取匹配，也就是说，该匹配不需要获取供以后使用。例如，"Windows(?=95\|98\|NT\|2000)"能匹配"Windows2000"中的"Windows"，但不能匹配"Windows3.1"中的"Windows"。预查不消耗字符，也就是说，在一个匹配发生后，在最后一次匹配之后立即开始下一次匹配的搜索，而不是从包含预查的字符之后开始。 |
| (?!pattern)  | 正向否定预查(negative assert)，在任何不匹配pattern的字符串开始处匹配查找字符串。这是一个非获取匹配，也就是说，该匹配不需要获取供以后使用。例如"Windows(?!95\|98\|NT\|2000)"能匹配"Windows3.1"中的"Windows"，但不能匹配"Windows2000"中的"Windows"。预查不消耗字符，也就是说，在一个匹配发生后，在最后一次匹配之后立即开始下一次匹配的搜索，而不是从包含预查的字符之后开始。 |
| (?<=pattern) | 反向(look behind)肯定预查，与正向肯定预查类似，只是方向相反。例如，"`(?<=95|98|NT|2000)Windows`"能匹配"`2000Windows`"中的"`Windows`"，但不能匹配"`3.1Windows`"中的"`Windows`"。 |
| (?<!pattern) | 反向否定预查，与正向否定预查类似，只是方向相反。例如"`(?<!95|98|NT|2000)Windows`"能匹配"`3.1Windows`"中的"`Windows`"，但不能匹配"`2000Windows`"中的"`Windows`"。 |
| x\|y         | 匹配 x 或 y。例如，'z\|food' 能匹配 "z" 或 "food"。'(z\|f)ood' 则匹配 "zood" 或 "food"。 |
| [xyz]        | 字符集合。匹配所包含的任意一个字符。例如， '[abc]' 可以匹配 "plain" 中的 'a'。 |
| [^xyz]       | 负值字符集合。匹配未包含的任意字符。例如， '[^abc]' 可以匹配 "plain" 中的'p'、'l'、'i'、'n'。 |
| [a-z]        | 字符范围。匹配指定范围内的任意字符。例如，'[a-z]' 可以匹配 'a' 到 'z' 范围内的任意小写字母字符。 |
| [^a-z]       | 负值字符范围。匹配任何不在指定范围内的任意字符。例如，'[^a-z]' 可以匹配任何不在 'a' 到 'z' 范围内的任意字符。 |
| \b           | 匹配一个单词边界，也就是指单词和空格间的位置。例如， 'er\b' 可以匹配"never" 中的 'er'，但不能匹配 "verb" 中的 'er'。 |
| \B           | 匹配非单词边界。'er\B' 能匹配 "verb" 中的 'er'，但不能匹配 "never" 中的 'er'。 |
| \cx          | 匹配由 x 指明的控制字符。例如， \cM 匹配一个 Control-M 或回车符。x 的值必须为 A-Z 或 a-z 之一。否则，将 c 视为一个原义的 'c' 字符。 |
| \d           | 匹配一个数字字符。等价于 [0-9]。                             |
| \D           | 匹配一个非数字字符。等价于 [^0-9]。                          |
| \f           | 匹配一个换页符。等价于 \x0c 和 \cL。                         |
| \n           | 匹配一个换行符。等价于 \x0a 和 \cJ。                         |
| \r           | 匹配一个回车符。等价于 \x0d 和 \cM。                         |
| \s           | 匹配任何空白字符，包括空格、制表符、换页符等等。等价于 [ \f\n\r\t\v]。 |
| \S           | 匹配任何非空白字符。等价于 [^ \f\n\r\t\v]。                  |
| \t           | 匹配一个制表符。等价于 \x09 和 \cI。                         |
| \v           | 匹配一个垂直制表符。等价于 \x0b 和 \cK。                     |
| \w           | 匹配字母、数字、下划线。等价于'[A-Za-z0-9_]'。               |
| \W           | 匹配非字母、数字、下划线。等价于 '[^A-Za-z0-9_]'。           |
| \xn          | 匹配 n，其中 n 为十六进制转义值。十六进制转义值必须为确定的两个数字长。例如，'\x41' 匹配 "A"。'\x041' 则等价于 '\x04' & "1"。正则表达式中可以使用 ASCII 编码。 |
| \num         | 匹配 num，其中 num 是一个正整数。对所获取的匹配的引用。例如，'(.)\1' 匹配两个连续的相同字符。 |
| \n           | 标识一个八进制转义值或一个向后引用。如果 \n 之前至少 n 个获取的子表达式，则 n 为向后引用。否则，如果 n 为八进制数字 (0-7)，则 n 为一个八进制转义值。 |
| \nm          | 标识一个八进制转义值或一个向后引用。如果 \nm 之前至少有 nm 个获得子表达式，则 nm 为向后引用。如果 \nm 之前至少有 n 个获取，则 n 为一个后跟文字 m 的向后引用。如果前面的条件都不满足，若 n 和 m 均为八进制数字 (0-7)，则 \nm 将匹配八进制转义值 nm。 |
| \nml         | 如果 n 为八进制数字 (0-3)，且 m 和 l 均为八进制数字 (0-7)，则匹配八进制转义值 nml。 |
| \un          | 匹配 n，其中 n 是一个用四个十六进制数字表示的 Unicode 字符。例如， \u00A9 匹配版权符号 (?)。 |



#### 运算符优先级

正则表达式从左到右进行计算，并遵循优先级顺序，这与算术表达式非常类似。

相同优先级的从左到右进行运算，不同优先级的运算先高后低。下表从最高到最低说明了各种正则表达式运算符的优先级顺序：

| 运算符                      | 描述                                                         |
| :-------------------------- | :----------------------------------------------------------- |
| \                           | 转义符                                                       |
| (), (?:), (?=), []          | 圆括号和方括号                                               |
| *, +, ?, {n}, {n,}, {n,m}   | 限定符                                                       |
| ^, $, \任何元字符、任何字符 | 定位点和序列（即：位置和顺序）                               |
| \|                          | 替换，"或"操作 字符具有高于替换运算符的优先级，使得"m\|food"匹配"m"或"food"。若要匹配"mood"或"food"，请使用括号创建子表达式，从而产生"(m\|f)ood"。 |



#### 测试实例解析

```
var str = "abcd test@runoob.com 1234";
var patt1 = /\b[\w.%+-]+@[\w.-]+\.[a-zA-Z]{2,6}\b/g;
document.write(str.match(patt1));
```

![img](https://www.runoob.com/wp-content/uploads/2014/03/regexp-metachar-2020-11-23.png)


---
title: "高阶函数专题"
date: "2020-02-16"
---

# JavaScript | 高阶函数专题

自古任何东西都是从低阶升上了高阶都是摇身一变从简单题变偏题难题、从具体变得抽象。

低阶可能只是一阶二阶，但高阶直接无穷无尽不可名状。然后从刚好踩在我还算能 hold 住的难度边界上飞入深空，一如我从来没能完全理解的数学分析与常微分方程......

还好编程语言中的高阶函数的概念没有那么的过分。

## 目录 <!-- omit in toc -->

- [概念](#概念)
  - [一个小栗子](#一个小栗子)
- [JS 自带的高阶函数](#js-自带的高阶函数)
  - [forEach() 方法](#foreach-方法)
  - [map() 方法](#map-方法)
  - [reduce() 方法](#reduce-方法)
  - [filter() 方法](#filter-方法)
  - [find() 方法](#find-方法)
  - [every() 方法](#every-方法)
  - [some() 方法](#some-方法)
  - [sort() 方法](#sort-方法)

<br>

---

<br>

## 概念

**高阶函数**（Higher-order Function）这个名字看起来很高端，实际上就是一种源于函数式编程的基本技术。

如果学习过 Python 的同学可能也会见过这个名词，在 JavaScript 中也是类似的，因为“函数能够当作变量值赋值给一个变量，变量保存了这个函数的引用”的特性，这使得函数同样可以作为函数的参数，传给另外一个函数。

这个“套娃”的行为中，能够接受函数作为参数的函数就被称为高阶函数。

### 一个小栗子

```js
const handle = function(val, fn) {
    return fn(val);
};

handle(233.3, Math.ceil); // 234
```

在上面的例子中，`handle`函数就是高阶函数，而`Math.ceil`则是回调函数。

虽然这个例子看起来`handle`函数干了多此一举的事情，但是我们可以在`handle`内对`val`参数执行更多的处理。

同时我们也可以注意到，它是那么容易理解而且随处可见——因为我们最常用的回调函数其实总是伴随着高阶函数，只是我们不知道它原来就是高阶函数而已。

<br>

## JS 自带的高阶函数

虽然这么一通~~废~~话下来，高阶函数看起来非常简单，但是 Javascript 自带的那些高阶函数的用法则不那么容易记住。

JavaScript 自带的常见的高阶函数方法有：

- `forEach()`
- `map()`
- `reduce()`
- `filter()`
- `find()` （ES6）
- `every()`
- `some()`
- `sort()`

可以看出，这些方法基本都应用于 Array 对象，而且大部分都来自于 ES5 及以上的标准。

虽然不了解这些函数，我们也能实现对应的功能，但如果借助它们，熟练的使用能大大简化我们的代码，提升代码性能，使我们的代码变得美观而专业。

（就算在平时的 coding 中不想用，这些自带的方法对于面试和写算法题仍然有不小的帮助）

> 至于`setTimeout`、`setInterval`之类的方法非常简单易懂，就不过多介绍了。

<br>

### forEach() 方法

`forEach()`应该是用得最多高阶函数之一，也非常好用。使用它可以遍历数组，调用回调函数处理数组的每一个元素。

**语法：**

```js
// 方括号表示为可选值
array.forEach(function(currVal[, index, array])[, thisVal])
```

**参数说明：**

- `function(currVal[, index, array])`  
  回调函数，会对数组的每个元素回调一次这个函数
  - `currVal`  
    当前正在处理的元素的值
  - `index`  
    当前正在处理的元素的下标值
  - `array`  
    就是`array`调用者自己
- `thisVal`  
  会用来设置回调函数的`this`值（因为匿名函数自己没有`this`值）  
  它很少会用到

`forEach()`没有返回值。

随便一个简单的**例子：**

```js
const nums = [2,3,5,7];

// 仅利用nums内保存的值
nums.forEach(num => console.log(num * 2)); // 4 6 10 14

// 想要改变nums内保存的值
nums.forEach((num, i, nums) => nums[i] = (num * 2)); // 4 6 10 14
```

> **注意：**`forEach()`不会对空数组进行检测，以下其他高阶函数大多也是如此。

除了 Array 对象，许多其他的对象也具有类似的`forEach()`方法可供使用（比如`NodeList`）。

`NodeList`对象使用`forEach()`方法，由于`NodeList`存储的是节点的引用，所以改变`currVal`会改变元素。

<br>

### map() 方法

`map()`方法由一个数组对象调用，接受一个回调函数，返回一个新数组，数组中的元素为原始数组元素调用回调函数处理后的值。

`map()`和`forEach()`很像，只不过它不改变原来的数组，而是把结果通过返回值保存利用。

**语法：**

```js
array.map(function(currVal[, index, array])[, thisVal])
```

**参数说明：**

- `function(currVal[, index, array])`  
  回调函数
  - `currVal`  
    当前正在处理的元素的值
  - `index`  
    当前正在处理的元素的下标值
  - `array`  
    调用者自己
- `thisVal`  
  设置回调函数的`this`值


例如，我们可以只用一行代码，把一个 number 数组的每一个元素开平方：

```js
let nums = [1, 4, 9, 16];
let sqrtedNums = nums.map(Math.sqrt);  // [1, 2, 3, 4]
```

<br>

### reduce() 方法

`reduce()`方法也是类似地，由数组调用，然后用回调函数处理每一个元素。

不同之处在于，它会把处理上一个元素时的返回值作为处理下一个元素的参数，最后返回的是一个值而不是一个数组。

**语法：**

```js
array.reduce(function(prevVal, currVal[, currIndex, array])[, initVal])
```

**参数说明：**

- `function(prevVal, currVal[, currIndex, array])`  
  回调函数
  - `prevVal`  
    处理前一个元素时返回的结果  
    如果没有设置`initVal`，则初值为第一个元素
  - `currVal`  
    当前正在处理的元素的值  
    如果没有设置`initVal`，则初值为第二个元素
  - `index`  
    当前正在处理的元素的下标值  
    如果没有设置`initVal`，则初值为1，否则为0
  - `array`  
    就是`array`调用者自己
- `initVal`  
  设置`prevVal`的初始值


一般教程中`reduce()`非常常见的例子是用于元素的累加：

```js
const nums = [1, 2, 3, 4];

let sum = nums.reduce((perv, curr) => perv + curr, 0);  // 0 + 1 + 2 + 3 + 4
sum = nums.reduce((perv, curr) => perv + curr);         // 1 + 2 + 3 + 4
/* 
 * `(perv, curr) => perv + curr`在这里等价于
 *
 * function(perv, curr) {
 *       return perv + curr;
 * }
 */
```

这么一说，好像恍惚间有着“递归函数”的既视感（当然，它只是实现了类似的效果）：

```js
function recursiveFunc(perv, curr, index, array) {
    const returnedVal = *一些操作*;
    return recursiveFunc(returnedVal, array[index + 1], array);
}
```

不过，单单简化了累加的代码是没有什么大用处的，我们的思维不要被这个普遍教程都会举例子限制住了，比如，`reduce()`还可以用于一些需要**两两比较**的操作：

```js
const nums = [1, 2, 3, 4];

// 求最大值
var max = nums.reduce((prev, curr) => Math.max(prev,curr));

// 数组去重
var newArr = arr.reduce((prev, curr) => {
    if (prev.indexOf(curr) === -1) {
        prev.push(curr);
    }
    return prev;
},[]);
```

<br>

### filter() 方法

`filter()`方法用于筛选数组中满足条件的元素，返回一个筛选后的新数组。

**语法：**

```js
array.filter(function(currVal[, index, array])[, thisVal])
```

**参数说明：**
 
- `function(currVal[, index, array])`  
  回调函数
  - `currVal`  
    当前正在处理的元素的值
  - `index`  
    当前正在处理的元素的下标值
  - `array`  
    调用者自己
- `thisVal`  
  设置回调函数的`this`值

这个方法确实非常直接，和字面意义一样——过滤（filter），回调函数判断条件后返回`boolean`值，`filter`会根据该值决定是否保留该值到筛选后的新数组里。

**例子：**

```js
const arr = [-5, -2, 0, 1];
// 取得数组的所有负数
const negativeNums = arr.filter((item, index, array) => item < 0);
console.log(negativeNums);   // [-2, -5]
```

### find() 方法

`find()`是 ES6 标准下的新方法，用法其实也很简单，就是`filter()`的单元素版——`find()`会判断数组内的每一个元素是否满足条件，并返回第一个满足该条件的元素。

> 看到介绍的第一时刻，我便想起了`document.querySelectorAll()`与`document.querySelector()`姐妹

**语法：**
 
```js
array.find(function(currVal[, index, array])[, thisVal])
```

**参数说明：**
 
- `function(currVal[, index, array])`  
  回调函数
  - `currVal`  
    当前正在处理的元素的值
  - `index`  
    当前正在处理的元素的下标值
  - `array`  
    调用者自己
- `thisVal`  
  设置回调函数的`this`值
 
**例子：**

```js
const arr = [-2, 0, 1, -3, 5];
// 取得数组中的第一个正数
const theFirstPositiveNum = arr.find((item, index, array) => item > 0);
console.log(theFirstPositiveNum);   // 1
```

<br>

### every() 方法

`every()`用于判断数组中的每一项元素是否都满足条件，返回一个布尔值。

**语法：**

```js
array.every(function(currVal[, index, array])[, thisVal])
```
**参数说明：**

- `function(currVal[, index, array])`  
  回调函数
  - `currVal`  
    当前正在处理的元素的值
  - `index`  
    当前正在处理的元素的下标值
  - `array`  
    调用者自己
- `thisVal`  
  设置回调函数的`this`值

可以看出是一个用来测试数组是否满足某种性质的方法。

**例子：**

```js
const arr = [-1, 0, 1, 3];
// 是否全部都大于0
const areAllGreaterThanZero = arr.every((item, index, array) => item > 0);
console.log(areAllGreaterThanZero);   // false
```

### some() 方法

和`every()`成对的一个方法。用于判断数组中的是否存在满足条件的元素，返回一个布尔值。

**语法：**

```js
array.some(function(currVal[, index, array])[, thisVal])
```

**参数说明：**

- `function(currVal[, index, array])`  
  回调函数
  - `currVal`  
    当前正在处理的元素的值
  - `index`  
    当前正在处理的元素的下标值
  - `array`  
    调用者自己
- `thisVal`  
  设置回调函数的`this`值

**例子：**

```js
const arr = [-1, 0, 1, 3];
// 是否存在一个数小于0
const isHasOnelessThanZero = arr.some((item, index, array) => item < 0);
console.log(isHasOnelessThanZero);   // true
```

<br>

### sort() 方法

> 这是一个很早就有的方法，所有的浏览器都支持`sort()`方法。

按照元素对应字符串的 Unicode code 的大小进行排序，默认升序。

**语法：**

```js
array.sort([function(first, second)])
```

**参数说明：**

- `function(first, second)`  
  用来指定按某种顺序进行排列的函数  
  如果省略，元素按照对应字符串的各个字符的Unicode位点进行排序（字符串比较大小算法）
  - `first`  
    第一个用于比较的元素
  - `second`  
    第二个用于比较的元素

注意到该方法是偏向于`string`而非`number`的，默认情况下是以字符串大小进行排序（排序规则不多赘述）：

```js
const arr = [1, 30, 4, 21, 1000];
console.log(arr.sort());
// 正：[1, 1000, 21, 30, 4]
// 误：[1, 4, 21, 30, 1000]  不是数字大小排序
// 误：[1000, 30, 21, 4, 1]  更不是降序
```

对于回调函数，如果返回值：

- 小于0，则`first`排在`second`的前面
- 等于0，则`first`与`second`相对位置不变
- 大于0，则`first`排在`second`的后面

所以想要按数字大小排序，简单的方法是用 a - b 的方法来计算，得到升序数组：

```js
function compareNumbers(a, b) {
    return a - b;
}
```

<br>

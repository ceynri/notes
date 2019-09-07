---
title: "JavaScript ES6 特性"
date: "2019-09-06"
---

# JavaScript | ES6 特性

*收集中*

## `...` 三点运算符

`...` 运算符用于操作数组，有两种层面：

第一个叫做 展开运算符(spread operator)，作用是和字面意思一样，就是把东西展开。可以用在array和object上都行。

比如:

```js
let a = [1,2,3];
let b = [0, ...a, 4]; // [0,1,2,3,4]

let obj = { a: 1, b: 2 };
let obj2 = { ...obj, c: 3 }; // { a:1, b:2, c:3 }
let obj3 = { ...obj, a: 3 }; // { a:3, b:2 }
```

第二个，第三个叫做 剩余操作符(rest operator)，是解构的一种，意思就是把剩余的东西放到一个array里面赋值给它。一般只针对array的解构，其他的没见过。。。

比如：

```js
let a = [1,2,3];
let [b, ...c] = a;
b; // 1
c; // [2,3]

// 也可以
let a = [1,2,3];
let [b, ...[c,d,e]] = a;
b; // 1
c; // 2
d; // 3
e; // undefined

// 也可以
function test(a, ...rest) {
  console.log(a); // 1
  console.log(rest); // [2,3]
}

test(1,2,3);
```

还有类似的：

```js
let array = [1, 2, 3, 4, 5];
const { x, y, ...z } = array;
// 其中z=[3, 4, 5]，注意如果由于array的length不足以完成析构，则会导致z为[]
```

对象：

```js
let obj = { name: 'zhangsan', age: 30, city: 'shenzhen' };
const {name, ...others} = obj;
console.log(name); // 'zhangsan'
console.log(others); // {age: 30, city: 'shenzhen'}
```

对象展开运算符， 可以称之为对象混合：

```js
let object = {
  a: '01', b: '02'
};

let newObject = {
  c: '03',
  ...object
};

console.log(newObject); //{c: "03", a: "01", b: "02"}
```

便捷的数组合并：

```js
let arr1 = ['Aixi', 'Bill'];
let arr2 = ['Cate'];
let arr3 = [...arr1, ...arr2];
console.log(arr3); // ["Aixi", "Bill", "Cate"]
```

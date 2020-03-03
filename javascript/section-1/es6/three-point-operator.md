---
title: "...运算符"
date: "2019-09-06"
---

# JavaScript | ...运算符

`...` 运算符有两种语法：展开语法、剩余语法。

## 目录 <!-- omit in toc -->

- [展开语法](#展开语法)
  - [在函数调用时](#在函数调用时)
  - [在构造数组时](#在构造数组时)
  - [在构造对象时](#在构造对象时)
- [剩余语法](#剩余语法)

<br>

---

<br>

## 展开语法

**展开语法**（spread syntax），可以将作用的对象在语法层面展开。用于函数调用或数组构造中时，可以将数组或者字符串进行展开；用于字面量对象的构造时，可以将对象变量以 key-value 的形式展开。

例子：

```js
// Function
function myFunc(a, b, c) {
  return a + b + c;
}
let arr = [1, 2, 3];
myFunc(...arr); // 6

// Array
let a = [1, 2, 3];
let b = [0, ...a, 4]; // [0,1,2,3,4]

// Object
let obj = { a: 1, b: 2 };
let obj2 = { ...obj, c: 3 }; // { a:1, b:2, c:3 }
let obj3 = { ...obj, a: 3 }; // { a:3, b:2 }
```

### 在函数调用时

使用展开语法，可以很好的代替部分原本需要使用`apply()`方法才能实现的效果：

```js
function myFunc(x, y, z) { 
    return x + y + z;
}
let args = [0, 1, 2];

myFunc(...args);
// 等价于
myFunc.apply(null, args);
```

而且展开语法可以和一般的变量并列一起用，所以某些情况下更加灵活。

```js
aFunc(1, ...args, -3, 0);
```

对于`new 构造函数`，想用`数组+apply`的方式是行不通的，这个时候使用`...数组`就非常的简洁方便了。

### 在构造数组时

学了展开语法后，我们可以使用`...`来代替传统的`slice`、`concat`等方法来实现更简洁的代码了。

比如数组拷贝：

```js
let arr = [1, 2, 3];
let arr2 = arr.slice();

// 等价于
let arr2 = [...arr]; 
```

数组合并：

```js
let arr1 = [0, 1, 2];
let arr2 = [3, 4, 5];
let arr3 = arr1.concat(arr2);

// 等价于
let arr3 = [...arr1, ...arr2];
```

### 在构造对象时

对象浅拷贝与对象合并：

```js
var obj1 = { foo: 'bar', x: 42 };
var obj2 = { foo: 'baz', y: 13 };

var clonedObj = { ...obj1 };
// { foo: "bar", x: 42 }

var mergedObj = { ...obj1, ...obj2 };
// { foo: "baz", x: 42, y: 13 }
```

<br>

## 剩余语法

**剩余语法**（rest syntax）可以把不定数量的、剩余的参数放到一个数组中，并赋值给`...`所作用的变量。

剩余语法可以看作是解构的一种，和展开语法的作用有一点“相反”的感觉。

例子：

```js
// 用于数组元素
let a = [1, 2, 3];
let [b, ...c] = a;
console.log(b); // 1
console.log(c); // [2, 3]

// 用于函数参数
function test(a, ...rest) {
  console.log(a); // 1
  console.log(rest); // [2, 3]
}
test(1, 2, 3);

// 用于对象属性
let obj = {
    name: 'zhangsan',
    age: 30,
    city: 'shenzhen'
};
const { name, ...others } = obj;
console.log(name); // 'zhangsan'
console.log(others); // { age: 30, city: 'shenzhen' }
```

<br>

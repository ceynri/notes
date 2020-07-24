---
title: "Class 类"
date: 2020-07-24
---

# JavaScript | Class 类

从语法层面支持面向对象编程，让 JavaScript 更容易上手。

<br>

## 对象、原型与类

在之前，当我们想要创建一个对象时，可以使用对象字面量：

```js
const person = {
  name: 'Lee',
  age: 24,
  profession: 'student',
  say() {
    console.log(`${this.age} years old, is a ${this.profession}`);
  }
}

person.say(); // 24 years old, is a student
```

这比较适合独立的对象。如果想要获得多个类似的对象，这样写就略显重复而麻烦了，使用构造函数来实现是一个比较好的选择：

```js
function Person(name, age, profession) {
  this.name = name;
  this.age = age;
  this.profession = profession;
}
Person.prototype.say = function() {
  console.log(`${this.age} years old, is a ${this.profession}`);
}

const haze = new Person('Haze', 18, 'programmer');
haze.say(); // 18 years old, is a programmer

const lee = new Person('Lee', 24, 'student');
lee.say(); // 24 years old, is a student
```

不过，对于习惯基于类的面向对象编程的 C++、Java 的同学，可能会对这种基于原型的面向对象编程会感到疑惑，在原型继承、动态修改原型等方面上，感到不方便且难读。实际上，原型相对类而言在某些方面更加灵活，不过这也导致原型显得更加复杂。

为了让 JavaScript 的面向对象编程更加简单，es6 标准规范引入了 class 语法来实现类似于一般语言的**基于类的面向对象编程**，熟悉 C++、Java 等语言很容易上手这种语法。

```js
class Person {
  // 构造器
  constructor(name, age, profession) {
    this.name = name;
    this.age = age;
    this.profession = profession;
  }
  // 方法
  say() {
    console.log(`${this.age} years old, is a ${this.profession}`);
  }
}

const lee = new Person('Lee', 24, 'student');
lee.say(); // 24 years old, is a student
```

> 对于没有接触过其他编程语言的同学要注意，class 内与 object 内并不一样，方法之间并不需要用逗号衔接

当我们执行 `new Person` 时，会调用 `constructor` 构造器，生成一个新的对象，这个名称是固定的。但我们的方法不用再显式绑定到 `Person.prototype` 上了，不论我们创建多少个 Person 的实例，`say()` 方法都只有一份，和绑定在 `prototype` 的表现相同。

<br>

## 语法

> 对于学习过其他语言的同学，语法基本是类似的，故不过多对细节进行讲解

### extends 继承

继承是扩展类的一种方式，让我们可以比较方便地在现有的类上增加新的属性与功能。

```js
class Driver extends Person {
  constructor(name, age, profession, car) {
    super(name, age, profession); // 必须在constructor的第一行调用
    this.drive(car);
  }
  drive(car) {
    console.log(`Driving ${car}...`);
  }
}

const driver = new Driver('ceynri', 18, 'driver', 'AE86'); // Driving AE86...
driver.say(); // 18 years old, is a driver
```

在 `constructor` 内调用 `super`，可以调用到父类的 `constructor`，将参数传给父类构造器，从而初始化父类继承来的属性。

如果子类没有显示的构造器，则会自动透传得到的参数：

```js
class Driver extends Person {
  // 没有 constructor 时，会自动增加以下逻辑
  // constructor(...args) {
  //   super(...args);
  // }
}
```

### 重写方法

子类可以重写父类方法，调用函数时会优先调用子类方法，如果想要调用父类方法，可以在类中使用 `super.methodName()`：

```js
class Driver extends Person {
  // ...

  say() {
    console.log('Don\'t talk when driving.');
    super.say();
  }
}
let driver = new Driver( ... );
driver.say(); // Don't talk when driving.
              // 18 years old, is a driver
```

### 字段

类字段（field）的概念类似于 C++/Java 里的成员函数，直接写在 class 里：

```js
class Person {
  
}
```

### 静态

我们可以在类的方法前增加 `static` 关键字进行修饰，得到的静态方法可以

<br>

## 本质与区别

实际上 class 类就是 JavaScript 基于原型继承的语法糖，类语法没有引入新的继承模型。

类仍然是一个函数（函数内容为 `constructor` 里的内容），而 method、getter 和 settor 都被写入该函数的 `prototype` 中。

不过，class 类在内部会有特殊的属性标记，使得它和一般的函数有着以下区别：

- 必须通过 `new` 来调用，否则会报错
- 将其以字符串输出时，形式仍然保持以 “class Xxx”作为开头
- 类方法不可枚举
- 内部自动使用 `use strict`

<br>

---
date: 2020-03-14
title: 二分法
---

# 二分法

二分法是在**已知有序的数组**中查找一个目标元素非常常见的搜索算法。

<br>

## 简介

二分法从概念上非常容易理解，就是利用了有序的性质，采用折半查找的方式，一次比较就可以排除掉当前范围内一半的元素，常用于代替线性查找的方法，降低时间复杂度至 O(logN)。

但是它虽然理解简单，实现起来却有非常多细节上的坑：循环条件要不要加“=”、mid该不该 +1/-1、if 的判断条件是...这些如果隔久了没记，下次在做题分分钟给你挂掉大部分边界样例。。

## 模板

二分法有多种写法，其中区间两边闭合`[left, right]`的写法比较容易理解（即 left 与 right 都在数组内），模板如下：

```js
function binarySearch(array, target) {
    let left = 0
    let right = array.length - 1
    // 开始查找
    while (left <= right) {
        const mid = Math.floor((left + right) / 2)
        if (array[mid] < target) {
            left = mid + 1
        } else if (array[mid] > target) {
            right = mid - 1
        } else {
            return mid
        }
    }
    // 循环下来都没有结果，说明没有找到
    return -1
}
```

因为 mid 是向下取整的缘故，所以区间左闭右开`[left, right)`的写法也是可以使用的，选择使用哪种就看个人喜好了。

```js
function binarySearch(array, target) {
    let left = 0
    let right = array.length // 注意

    while (left < right) { // 注意
        let mid = Math.floor((left + right) / 2)
        if (array[mid] < target) {
            left = mid + 1
        } else if (array[mid] > target) {
            right = mid // 注意
        } else {
            return mid
        }
    }
    return -1
}
```

## 变种

有些题目并不会那么简单。例如`[1, 2, 2, 2, 3]`这样一个数组，如果我们想要找`2`，使用二分法我们可以找到三个`2`的中间那个，但如果题目要求我们找到数组最刚开始出现的`2`或者是最后出现的`2`，我们虽然可以以中间这个`2`为起点左/右线性查找，但这就不能保证 O(logN) 的时间复杂度了。所以我们可以对二分法进行改进，模板如下：

```js
// 找到第一个target
function binarySearchLeft(array, target) {
    let left = 0
    let right = array.length - 1

    while (left <= right) {
        const mid = Math.floor((left + right) / 2)
        if (array[mid] < target) {
            left = mid + 1
        } else { // >= target
            right = mid - 1 // 注意
        }
    }
    // 如果没有越界，且找到了target
    if (left < array.length && array[left] === target) {
        return left
    }
    return -1
}

// 找到最后一个target
function binarySearchRight(array, target) {
    let left = 0
    let right = array.length - 1

    while (left <= right) {
        const mid = Math.floor((left + right) / 2)
        if (array[mid] > target) {
            right = mid - 1
        } else { // <= target
            left = mid + 1
        }
    }
    // 如果没有越界，且找到了target
    if (right > 0 && array[right] === target) {
        return right
    }
    return -1
}
```

<br>

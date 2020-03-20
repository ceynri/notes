---
date: 2020-03-20
title: 排序算法
---

# 排序算法

每一个科班生必学的十种排序算法，虽然面试好像考的不多，但构思算法的原理之精巧值得回味。

<br>

> 预定义：
> ```js
> // 数组元素交换
> function swap(arr, i, j) {
>     [arr[i], arr[j]] = [arr[j], arr[i]];
> }

## 冒泡排序

### 标签

- 两两交换
- 时间复杂度 O(n^2)
- 空间复杂度 O(1)
- 稳定

### 流程

- 将数组视作为未排序的部分 `[0, i]` 和已排序的部分 `(i, arr.length)`
- 相邻元素 `arr[j]`、`arr[j + 1]` 两两比对
- 如果与期望排序顺序相反 `(arr[j] > arr[j + 1]) === true`
  - 交换它们
- 每一轮选出未排序部分的最大的元素放在未排序元素的末尾，下一轮需要排序的元素个数减少（`--i`）。

### 代码

```js
function bubbleSort(arr) {
    for (let i = arr.length - 1; i > 0; --i) {
        // 优化：如果一轮下来没有任何交换，说明已经完全有序
        let hadSwap = false;

        for (let j = 0; j < i; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr, j, j + 1);
                hadSwap = true;
            }
        }
        if (hadSwap) {
            break;
        }
    }
    return arr;
}
```

<br>

## 选择排序

### 标签

- 每次选择一个最小的
- 时间复杂度 O(n^2)
- 空间复杂度 O(1)
- 不稳定

### 流程

- 将数组视作已排序的部分 `[0, i]` 和未排序的部分 `(i, arr.length)`
- 遍历一遍未排序部分 `(i, arr.length)`，找到最小的元素 `arr[minIndex]`
- 将最小的元素与未排序部分的第一个元素 `arr[i]` 交换
- 已排序部分的元素个数增加（`i++`）

### 代码

```js
function selectionSort(arr) {
    for (let i = 0; i < arr.length - 1; i++) {
        let minIndex = i;
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        swap(arr, i, minIndex);
    }
    return arr;
}
```

<br>

## 直接插入排序

### 标签

- 扑克牌排序
- 选一个未排序的牌插入到已排好的牌组中
- 时间复杂度 O(n^2)
- 空间复杂度 O(1)
- 稳定

### 流程

以扑克牌为例：

- 将牌组视作已整理好的牌组 `[0, i]` 和未整理好的牌组 `(i, card.length)`
- 取走一张牌 `cards[i]`
- 从这张取走的牌往前找比这张牌要小的牌
  - 比取走的牌要大的牌，需要往后拨（`cards[j + 1] = cards[j]`）
- 将取走的牌插在比它小的牌的后面
- 已整理好的牌增加（`i++`）

### 代码

```js
function insertionSort(cards) {
    for (let i = 1; i < cards.length; i++) {
        // 取走一张牌
        const card = cards[i];
        let j = i - 1;
        // 前面的牌比取走的牌大
        while (j >= 0 && cards[j] > card) {
            // 大牌往后推
            cards[j + 1] = cards[j];
            j--;
        }
        // 将牌插到比这张牌要小的牌的后面
        cards[j + 1] = card;
    }
    return cards;
}
```

<br>

## 希尔排序

### 标签

- 分组插入排序
- 相同间隔的元素一组，间隔逐渐减小
- 时间复杂度 O(n^1.3) ~ O(n^2)
- 空间复杂度 O(1)
- 不稳定

### 流程

- 取一个小于数组大小的正整数 `gap`
- 把所有序号相隔 `gap` 大小的数组元素放一组
  - 组内进行直接插入排序
- 减小 `gap` 值，重复上述分组和排序操作
- `gap = 1` 时，执行完此轮插入排序后即完成了整个希尔排序

> 具体先略了，日后感兴趣再补

<br>

## 归并排序

### 标签

- 分而治之
- 拿空间换时间
- 时间复杂度 O(nlogn)
- 空间复杂度 O(n)
- 稳定

### 流程

- 分
  - 将数组一分为二
  - 被切分的一半继续一分为二，直到无法切分
  - 将被切分的元素们两两合并
- 合
  - 对比两个无法被切分的元素的大小
    - 小的在前，大的在后，得到一个有序的小数组
  - 继续递归，将两个有序的小数组分别从小到大取一个元素

### 代码

```js
function mergeSort(arr) {
    if (arr.length < 2) {
        return arr;
    }
    const middle = Math.floor(arr.length / 2);
    const left = arr.slice(0, middle);
    const right = arr.slice(middle);
    return merge(mergeSort(left), mergeSort(right));
}

function merge(left, right) {
    let result = [];
    let i = 0;
    let j = 0;
    while (i < left.length && j < right.length) {
        result.push((left[i] <= right[j]) ? left[i++] : right[j++]);
    }
    while (i < left.length) {
        result.push(left[i++]);
    }
    while (j < right.length) {
        result.push(right[j++]);
    }
    return result;
}
```

<br>

## 排序

### 标签

- 
- 时间复杂度 O(n^2)
- 空间复杂度 O(1)
- 稳定

### 流程

- 

### 代码

```js
function Sort(arr) {
    for (let i = arr.length - 1; i > 0; --i) {
        for (let j = 0; j < i; j++) {

        }
    }
    return arr;
}
```

<br>

## 排序

### 标签

- 
- 时间复杂度 O(n^2)
- 空间复杂度 O(1)
- 稳定

### 流程

- 

### 代码

```js
function Sort(arr) {
    for (let i = arr.length - 1; i > 0; --i) {
        for (let j = 0; j < i; j++) {

        }
    }
    return arr;
}
```

<br>

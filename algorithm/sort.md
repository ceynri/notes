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
> function swap(array, i, j) {
>     [array[i], array[j]] = [array[j], array[i]];
>     return array;
> }

## 冒泡排序

### 标签

- 两两交换
- 时间复杂度 O(n^2)
- 空间复杂度 O(1)
- 稳定
- 适合基本有序的数组排序（时间复杂度降低至 O(n)）

### 流程

- 将数组视作为未排序的部分 `[0, i]` 和已排序的部分 `(i, array.length)`
- 相邻元素 `array[j]`、`array[j + 1]` 两两比对
- 如果与期望排序顺序相反 `(array[j] > array[j + 1]) === true`
  - 交换它们
- 每一轮选出未排序部分的最大的元素放在未排序元素的末尾，下一轮需要排序的元素个数减少（`--i`）。

### 代码

```js
function bubbleSort(array) {
    for (let i = array.length - 1; i > 0; --i) {
        // 优化：如果一轮下来没有任何交换，说明已经完全有序
        let hadSwap = false;

        for (let j = 0; j < i; j++) {
            if (array[j] > array[j + 1]) {
                swap(array, j, j + 1);
                hadSwap = true;
            }
        }
        if (hadSwap) {
            break;
        }
    }
    return array;
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

- 将数组视作已排序的部分 `[0, i]` 和未排序的部分 `(i, array.length)`
- 遍历一遍未排序部分 `(i, array.length)`，找到最小的元素 `array[minIndex]`
- 将最小的元素与未排序部分的第一个元素 `array[i]` 交换
- 已排序部分的元素个数增加（`i++`）

### 代码

```js
function selectionSort(array) {
    for (let i = 0; i < array.length - 1; i++) {
        let minIndex = i;
        for (let j = i + 1; j < array.length; j++) {
            if (array[j] < array[minIndex]) {
                minIndex = j;
            }
        }
        swap(array, i, minIndex);
    }
    return array;
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
- 多种 O(n^2) 时间复杂度算法里速度最快的
- 数据量不大时的优选

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
- 追求既快速又具备稳定性且不考虑内存占用时的优选

### 流程

- 分
  - 将数组一分为二
  - 被切分的一半继续一分为二，直到无法切分
  - 将被切分的元素们两两合并为一个已排序的数组
- 治
  - 对比两个无法被切分的元素的大小
    - 小的在前，大的在后，得到一个有序的小数组
  - 继续递归，将相邻的两个有序小数组合并为一个有序的数组

### 代码

```js
function mergeSort(array) {
    // 如果不可再分
    if (array.length < 2) {
        return array;
    }
    // 对半分
    const middle = Math.floor(array.length / 2);
    const left = array.slice(0, middle);
    const right = array.slice(middle);
    // 将对半分的两个数组合并为一个有序的数组
    return merge(mergeSort(left), mergeSort(right));
}

function merge(left, right) {
    const result = [];
    let i = 0;
    let j = 0;
    // 双指针，谁小先取谁
    while (i < left.length && j < right.length) {
        result.push((left[i] <= right[j]) ? left[i++] : right[j++]);
    }
    // 合并未取完元素（以下两个while只会执行其中一个）
    while (i < left.length) {
        result.push(left[i++]);
    }
    while (j < right.length) {
        result.push(right[j++]);
    }
    // 返回包含left和right所有元素的有序数组
    return result;
}
```

<br>

## 快速排序

### 标签

- 最出名、最厉害
- 时间复杂度 O(nlogn)
- 空间复杂度 O(logn)
- 不稳定

### 流程

快速排序有很多种实现方法，这里讲其中一种比较经典的实现方式：

- 从数组中取一个基准数 `pivot`
  - 可以取第一位数（十分简易，但数组大致有序时，时间复杂度飙升至O(n^2)）
  - 也可以取随机数（避免上述情况）
  - 推荐取中位数（避免随机数导致的同数组排序速度有波动的问题）
- 将基准数交换到开头
- 使用双指针 `low`、`high` 分别指向开头与结尾
- 双指针交替向对方靠拢：
  - `high` 不断向 `low` 靠拢，当 `high` 找到小于 `pivot` 的元素时停下
  - 然后 `low` 不断向 `high` 靠拢，当 `low` 找到大于 `pivot` 的元素时停下
  - 这时候就有了一对逆序的元素
  - 将它们两个交换位置，使得相对符合期望顺序
  - 重复以上行为
  - 直到 `low == high`：
    - 此时 `low`（`high`） 一定比 `pivot` 小（后面会说明原因）
    - 交换 `low` 与 `pivot`
- 此时基数在整个数组中的位置被唯一确定
- 再对基数左边与右边的两份未排序数组重复上面的算法即可

`low == high` 时所指向元素一定小于 `pivot` 的理由：

- 循环的一开始 `low` 并未移动，所以 `low <= pivot`
- 而因为是 `high` 先向 `low` 靠拢，所以停下时一定有 `high <= pivot`
  - 这个位置可能是 `high == low`
    - 所以 `high == low <= pivot`
    - **循环结束**
  - 如果不是，也有 `high < pivot`
  - 则让 `low` 向 `high` 移动，当停下时：
    - 如果 `low == high`
      - 因为`high < pivot`，所以 `low < pivot`
      - **循环结束**
    - 如果停在比 `pivot` 基数大的位置，则循环未结束

### 代码

```js
function quickSort(array, start = 0, end = array.length - 1) {
    if (array.length > 1 && start < end) {
        // 通过快排算法确定一个元素在整个数组中的位置
        const index = devide(array, start, end);
        // 对这个被确定好位置的元素的左右两部分元素递归执行快排
        quickSort(array, start, index - 1);
        quickSort(array, index + 1, end);
    }
    return array;
}

function devide(array, low, high) {
    // 将中间数作为基数，并将基数移到开头
    // 如果只取第一位数作为基数，则可以注释掉下面这行代码
    swap(array, Math.floor((low + high) / 2), low);
    // 记录基数的下标
    const pivot = low;

    while (low < high) {
        // 从后面往前找到一个小于基准的下标
        while (array[high] >= array[pivot] && low < high) {
            high--;
        }
        // 从前面往后找到一个大于基准的下标
        while (array[low] <= array[pivot] && low < high) {
            low++;
        }
        // 交换这两个元素，使得小的元素在前面，大的元素在后面
        if (low < high) {
            swap(array, low, high);
        }
    }
    // low与high相等时，必定停留在比pivot所指向的基数小的元素上
    swap(array, pivot, low);

    // 循环结果：
    // 所有比基数小的元素都在基数的前面
    // 所有比基数大的元素都在基数的后面
    // 基数在这整个数组中的位置被确定下来
    // 返回基数的下标（low或者high都是一样的）
    return low;
}
```

另一种写法，借用了滑动窗口的思想，更加精巧：

```js
function quickSort(array, start = 0, end = array.length - 1) {
    if (array.length > 1 && start < end) {
        const index = partition(array, start, end);
        quickSort(array, start, index - 1);
        quickSort(array, index + 1, end);
    }
    return array;
}

function partition(array, low, high) {
    const end = high;
    // 将中数移到开头
    swap(array, Math.floor((low + high) / 2), low);
    // 取中数作为基准数
    // 要排序的数里不包含基准数（所以low++），最后会再将基准数插回去
    const pivot = low++;

    // 构建一个滑动窗口[low, high]，窗口里的数都满足大于等于基准数的条件
    for (let high = low; high <= end; high++) {
        // 小于基准数的数会被丢到滑动窗口的前面
        if (array[high] < array[pivot]) {
            swap(array, low++, high);
        }
    }
    // 将pivot与窗口的前面一格的元素交换，使得左边元素小于pivot，右边元素大于pivot
    swap(array, pivot, low - 1);
    // 返回pivot的下标
    return low - 1;
}
```

<br>

## 堆排序

### 标签

- 
- 时间复杂度 O(n^2)
- 空间复杂度 O(1)
- 稳定

### 流程

- 

### 代码

```js
function Sort(array) {
    for (let i = array.length - 1; i > 0; --i) {
        for (let j = 0; j < i; j++) {

        }
    }
    return array;
}
```

<br>

## 计算排序

## 桶排序

## 基数排序

---
title: "LeetCode 题解速览"
date: "2020-03-27"
---

# LeetCode 题解速览

对于写过的题，将其最精华的思想浓缩为一句 key，组成 key list，以最后复习时过一遍这些思想。

> **⚠ 整理中**
> 
> 最近日期：04/14
> 
> 之前做过的题目补充题解的进度：85%
> 
> 手动整理太慢，简单写了一份代码用于获得所有已通过的题目信息并生成markdown表格
> 
> 有需要可以自取，根据你的需求改一改就好了
> 
> ```js
> // 打开 https://leetcode-cn.com/problemset/all/
> // 登录后，拉到页面最低端，将“每页数量”设置为全部
> // 在控制台运行以下代码，即可自动生成完成过的题目markdown表格
> let resultArray = [
>     '| 序号 | 难度 | 题目 | 标签 | 思路 |',
>     '| ---- | ---- | ---- | ---- | ---- |'
> ];
> let table = document.querySelector('.reactable-data');
> for (let row of table.children) {
>     if (row.querySelector('.text-success')) {
>         let cols = row.querySelectorAll('td');
>         let order = cols[1].innerHTML;
>         let title = row.querySelector('.question-title a');
>         let titleName = title.innerHTML;
>         let titleLink = title.getAttribute('href');
>         let level = cols[5].querySelector('span').innerHTML;
>         resultArray.push(`| ${order} | ${level} | [${titleName}](https://leetcode-cn.com${titleLink}) |  |  |`);
>     }
> }
> let resultString = resultArray.join('\n');
> console.log('复制内容：');
> console.log(resultString);
> alert('请手动复制监控台输出的内容');
> ```

<br>

## 1~500

| 序号 | 难度 | 题目                                                                                                         | 标签        | 思路                                                         |
| ---- | ---- | ------------------------------------------------------------------------------------------------------------ | ----------- | ------------------------------------------------------------ |
| 1    | 简单 | [两数之和](https://leetcode-cn.com/problems/two-sum/)                                                        | 数组        | 利用哈希表的key，使key+value=target                          |
| 2    | 中等 | [两数相加](https://leetcode-cn.com/problems/add-two-numbers/)                                                | 链表        | 进位状态、3while循环                                         |
| 8    | 中等 | [字符串转换整数 (atoi)](https://leetcode-cn.com/problems/string-to-integer-atoi/)                            | 字符串 正则 | 正则匹配 `/^(-|\+)?\d+/`                                     |
| 11   | 中等 | [盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/)                                | 数组 贪心   | 短板决定高度：两板中较短一版向中心找更长的板                 |
| 21   | 简单 | [合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)                                 | 链表        | -                                                            |
| 22   | 中等 | [括号生成](https://leetcode-cn.com/problems/generate-parentheses/)                                           | 回溯        | 还有'('时就插入'('，回溯，剩余')'多于'('就插入')'            |
| 24   | 中等 | [两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs)                                 | 链表        | 两两一组，每次记录前一组的最后一个                           |
| 28   | 简单 | [实现 strStr()](https://leetcode-cn.com/problems/implement-strstr)                                           | 字符串      | 暴力 / Sunday / KMP                                          |
| 36   | 中等 | [有效的数独](https://leetcode-cn.com/problems/valid-sudoku)                                                  | 数组        | 用三个对象数组，空间换时间，可仅一次遍历                     |
| 42   | 困难 | [接雨水](https://leetcode-cn.com/problems/trapping-rain-water/)                                              | 数组 记忆化 | 遍历两次，记下每个元素的左最高元素和右最高元素，然后取交集   |
| 42   | -    | -                                                                                                            | 数组 栈     | 高度向下时压栈，向上时元素出栈并与当前元素计算水槽宽高       |
| 42   | -    | -                                                                                                            | 数组 双指针 | 从两边各自记录找到的最大值，矮的一边向中遍历，小于最大可倒水 |
| 55   | 中等 | [跳跃游戏](https://leetcode-cn.com/problems/jump-game/)                                                      | 数组 贪心   | 一步一步走，不断延拓我们能够达到的最大边界                   |
| 56   | 中等 | [合并区间](https://leetcode-cn.com/problems/merge-intervals/)                                                | 数组        | 先以起始位置排序，再按顺序比较，接壤则合并                   |
| 72   | 困难 | [编辑距离](https://leetcode-cn.com/problems/edit-distance/)                                                  | 动态规划    | 二维动归，抽象出三种修改方式的状态转移关系                   |
| 74   | 中等 | [搜索二维矩阵](https://leetcode-cn.com/problems/search-a-2d-matrix)                                          | 数组 查找   | 二维的二分法，`[row, col] = [floor(mid/n), mid%n]`           |
| 88   | 简单 | [合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array)                                      | 数组        | 逆向思维，从后往前两两比较可以让出位置                       |
| 94   | 中等 | [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)                          | 树          | 左遍历压栈到底，弹出节点值，取其右节点继续左遍历             |
| 100  | 简单 | [相同的树](https://leetcode-cn.com/problems/same-tree/)                                                      | 树          | 选一种遍历方式同时遍历两棵树即可                             |
| 121  | 简单 | [买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock)                       | 数组        | 线性遍历，记录当前已知最小值，相减以计算最大利润             |
| 122  | 简单 | [买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii)                 | 数组        | 相邻相减，如果是正的就加起来                                 |
| 144  | 中等 | [二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)                         | 树          | 取节点值，右树压栈，往左树探                                 |
| 151  | 中等 | [翻转字符串里的单词](https://leetcode-cn.com/problems/reverse-words-in-a-string/)                            | 字符串      | split -> reverse -> join                                     |
| 169  | 简单 | [多数元素](https://leetcode-cn.com/problems/majority-element)                                                | 数组        | 哈希表统计出现次数，某一值出现次数过半数则结束               |
| 175  | 简单 | [组合两个表](https://leetcode-cn.com/problems/combine-two-tables)                                            | SQL JOIN    | `A left join B on A.key = B.key`                             |
| 206  | 简单 | [反转链表](https://leetcode-cn.com/problems/reverse-linked-list)                                             | 链表        | prev、current、current.next 三角恋                           |
| 225  | 简单 | [用队列实现栈](https://leetcode-cn.com/problems/implement-stack-using-queues)                                | 队列 设计   | 前n-1个数从队头出来返入队尾，原本的队尾即可从队头取出        |
| 227  | 中等 | [基本计算器 II](https://leetcode-cn.com/problems/basic-calculator-ii)                                        | 设计        | 加减直接运算，乘除则先把之前加减的给吐出来运算完了再加回去   |
| 235  | 简单 | [二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) | 二叉搜索树  | 利用搜索树性质，找到值在两数之间的数即可                     |
| 289  | 中等 | [生命游戏](https://leetcode-cn.com/problems/game-of-life/)                                                   | 矩阵 卷积   | 状态值少，可以使用位运算，在不同的位保存不同阶段的状态       |
| 300  | 中等 | [最长上升子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence)                            | 动态规划    | 后面的dp从前面符合条件的dp取最大                             |
| 300  | -    | -                                                                                                            | 贪心 二分法 | 维护一个序列：大的接在后面，小的找个位置挤掉一个相对大的     |
| 322  | 中等 | [零钱兑换](https://leetcode-cn.com/problems/coin-change)                                                     | 动态规划    | `dp[i] = Math.min(dp[i], dp[i - coin] + 1)`                  |
| 322  | -    | -                                                                                                            | 贪心 回溯   | 每次贪心地选择尽量大的硬币（需回溯所有情况以保证最优）       |
| 355  | 中等 | [设计推特](https://leetcode-cn.com/problems/design-twitter/)                                                 | 设计        | 使用哈希表、链表、优先队列以尽量低的复杂度解决多路归并问题   |
| 357  | 中等 | [计算各个位数不同的数字个数](https://leetcode-cn.com/problems/count-numbers-with-unique-digits)              | 数学        | 数的排列组合                                                 |
| 365  | 中等 | [水壶问题](https://leetcode-cn.com/problems/water-and-jug-problem)                                           | 遍历        | 遍历所有操作，消除重复情况以避免死循环                       |
| 365  | -    | -                                                                                                            | 数学        | 存在 a、b 使得`ax + by = z`，即满足`z % gcd(x, y) = 0`       |
| 404  | 简单 | [左叶子之和](https://leetcode-cn.com/problems/sum-of-left-leaves/)                                           | 树          | 给函数增加一个“当前节点是否为左节点”的标记                   |
| 409  | 简单 | [最长回文串](https://leetcode-cn.com/problems/longest-palindrome)                                            | 哈希表      | 偶数个数字符直接对称，奇数个可丢掉一个变成偶数个加以利用     |
| 445  | 中等 | [两数相加 II](https://leetcode-cn.com/problems/add-two-numbers-ii/)                                          | 链表        | 遇到逆序，可以考虑栈                                         |
| 460  | 困难 | [LFU缓存](https://leetcode-cn.com/problems/lfu-cache/)                                                       | 设计 哈希表 | 双哈希表以不同的key记录同一个结果，以维护O(1)的增与查        |

## 501~1000

| 序号 | 难度 | 题目                                                                                                    | 标签          | 思路                                                          |
| ---- | ---- | ------------------------------------------------------------------------------------------------------- | ------------- | ------------------------------------------------------------- |
| 501  | 简单 | [二叉搜索树中的众数](https://leetcode-cn.com/problems/find-mode-in-binary-search-tree/)                 | 二叉搜索树    | 利用“中序遍历BST可得到递增数组”的性质                         |
| 509  | 简单 | [斐波那契数](https://leetcode-cn.com/problems/fibonacci-number)                                         | 动态规划      | 非常经典的动规消除重复子问题 `dp[i] = dp[i - 1] + dp[i - 2]`  |
| 513  | 中等 | [找树左下角的值](https://leetcode-cn.com/problems/find-bottom-left-tree-value/)                         | 树            | 记录当前遍历的深度，最深的最左叶子总是会第一个遍历到          |
| 542  | 中等 | [01 矩阵](https://leetcode-cn.com/problems/01-matrix/)                                                  | 矩阵 遍历     | 逆向思维，将“每个1都去找最近的0”变成“所有0组成超级源点去BFS”  |
| 543  | 简单 | [二叉树的直径](https://leetcode-cn.com/problems/diameter-of-binary-tree)                                | 树 遍历       | 记录左树和右树高，记录最大的左右树高之和，返回1+最高子树高    |
| 599  | 简单 | [两个列表的最小索引总和](https://leetcode-cn.com/problems/minimum-index-sum-of-two-lists)               | 哈希表        | 将其中一表用\<list[i], i>存为哈希表，另一表线性遍历即可       |
| 643  | 简单 | [子数组最大平均数 I](https://leetcode-cn.com/problems/maximum-average-subarray-i)                       | 数组          | 定宽滑动窗口                                                  |
| 695  | 中等 | [岛屿的最大面积](https://leetcode-cn.com/problems/max-area-of-island)                                   | 矩阵 遍历     | 典型矩阵DFS，每个位置做好visited标记后探索四个方向            |
| 744  | 简单 | [寻找比目标字母大的最小字母](https://leetcode-cn.com/problems/find-smallest-letter-greater-than-target) | 数组 查找     | 尤其注意数组具有一个“有序”的条件，采取线性遍历或二分法        |
| 747  | 简单 | [至少是其他数字两倍的最大数](https://leetcode-cn.com/problems/largest-number-at-least-twice-of-others)  | 数组          | 线性遍历找到第一大和第二大的数进行比较即可                    |
| 836  | 简单 | [矩形重叠](https://leetcode-cn.com/problems/rectangle-overlap)                                          | 几何          | max(x1, x3) < min(x2, x4) && max(y1, y3) < min(y2, y4)        |
| 838  | 中等 | [推多米诺](https://leetcode-cn.com/problems/push-dominoes)                                              | 数组 双指针   | 双指针根据不同的情况进行区域划分，对区域做对应的操作          |
| 841  | 中等 | [钥匙和房间](https://leetcode-cn.com/problems/keys-and-rooms)                                           | 遍历          | DFS/BFS，把当前进入的房间内未去过的房间的钥匙拿到             |
| 876  | 简单 | [链表的中间结点](https://leetcode-cn.com/problems/middle-of-the-linked-list)                            | 链表          | 经典快慢指针                                                  |
| 887  | 困难 | [鸡蛋掉落](https://leetcode-cn.com/problems/super-egg-drop/)                                            | 动态规划 二分 | dp(K,N)=1+min(max(dp(K-1,X-1),dp(K,N-X))) K蛋数 N层数 X当前层 |
| 892  | 简单 | [三维形体的表面积](https://leetcode-cn.com/problems/surface-area-of-3d-shapes)                          | 几何          | 注意不能用三视图算 可先算所有立方体的表面积再减去被遮挡的面   |
| 905  | 简单 | [按奇偶排序数组](https://leetcode-cn.com/problems/sort-array-by-parity)                                 |               |                                                               |
| 912  | 中等 | [排序数组](https://leetcode-cn.com/problems/sort-an-array/)                                             | 排序          | 任意实现一种排序                                              |
| 914  | 简单 | [卡牌分组](https://leetcode-cn.com/problems/x-of-a-kind-in-a-deck-of-cards)                             |               |                                                               |
| 938  | 简单 | [二叉搜索树的范围和](https://leetcode-cn.com/problems/range-sum-of-bst)                                 |               |                                                               |
| 945  | 中等 | [使数组唯一的最小增量](https://leetcode-cn.com/problems/minimum-increment-to-make-array-unique)         |               |                                                               |
| 958  | 中等 | [二叉树的完全性检验](https://leetcode-cn.com/problems/check-completeness-of-a-binary-tree)              |               |                                                               |
| 994  | 简单 | [腐烂的橘子](https://leetcode-cn.com/problems/rotting-oranges)                                          |               |                                                               |
| 999  | 简单 | [可以被一步捕获的棋子数](https://leetcode-cn.com/problems/available-captures-for-rook)                  |               |                                                               |

## 1000+

| 序号 | 难度 | 题目                                                                                                           | 标签               | 思路                 |
| ---- | ---- | -------------------------------------------------------------------------------------------------------------- | ------------------ | -------------------- |
| 1013 | 简单 | [将数组分成和相等的三个部分](https://leetcode-cn.com/problems/partition-array-into-three-parts-with-equal-sum) |                    |                      |
| 1071 | 简单 | [字符串的最大公因子](https://leetcode-cn.com/problems/greatest-common-divisor-of-strings)                      |                    |                      |
| 1103 | 简单 | [分糖果 II](https://leetcode-cn.com/problems/distribute-candies-to-people)                                     |                    |                      |
| 1111 | 中等 | [有效括号的嵌套深度](https://leetcode-cn.com/problems/maximum-nesting-depth-of-two-valid-parentheses-strings/) | 字符串 子序列 分组 | 利用奇偶性进行分组   |
| 1160 | 简单 | [拼写单词](https://leetcode-cn.com/problems/find-words-that-can-be-formed-by-characters)                       |                    |                      |
| 1162 | 中等 | [地图分析](https://leetcode-cn.com/problems/as-far-from-land-as-possible/)                                     | 图 遍历            | 多源DFS，visited数组 |

## 程序员面试金典系列

| 序号         | 难度 | 题目                                                                    | 标签      | 思路                                                   |
| ------------ | ---- | ----------------------------------------------------------------------- | --------- | ------------------------------------------------------ |
| 面试题 01.06 | 简单 | [字符串压缩](https://leetcode-cn.com/problems/compress-string-lcci)     | 字符串    | 取一字符，while自增循环计其连续个数，加入结果字符串    |
| 面试题 01.07 | 中等 | [旋转矩阵](https://leetcode-cn.com/problems/rotate-matrix-lcci/)        | 矩阵 交换 | 分成4区，顺时针交换；或者先转置，再水平翻转            |
| 面试题 04.03 | 中等 | [特定深度节点链表](https://leetcode-cn.com/problems/list-of-depth-lcci) | 树 遍历   | 层次遍历（BFS）一层一次循环或者DFS将深度当参数传入     |
| 面试题 10.01 | 简单 | [合并排序的数组](https://leetcode-cn.com/problems/sorted-merge-lcci)    | 数组      | 类似归并，要点是从后往前遍历，从尾巴开始填充           |
| 面试题 16.03 | 困难 | [交点](https://leetcode-cn.com/problems/intersection-lcci/)             | 数学      | 参数方程表示线段，求交点，考虑斜率相等重叠等情况       |
| 面试题 17.16 | 简单 | [按摩师](https://leetcode-cn.com/problems/the-masseuse-lcci)            | 动态规划  | dp[i]=max(dp[i-1], dp[i-2]+val[i])（三个变量迭代即可） |

## 剑指Offer系列

| 序号          | 难度 | 题目                                                                                                          | 标签      | 思路                                                    |
| ------------- | ---- | ------------------------------------------------------------------------------------------------------------- | --------- | ------------------------------------------------------- |
| 面试题10- I   | 简单 | [斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof)                                    | 数学      | 基础题，直接用两个变量递推就可以                        |
| 面试题11      | 简单 | [旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof)              | 数组 查找 | 二分查找的变种，注意两指针相等时需要做保守策略          |
| 面试题13      | 中等 | [机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)                      | 矩阵 遍历 | DFS/BFS 仔细分析限制条件，只需向右/下走即可遍历所有     |
| 面试题14- I   | 中等 | [剪绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof)                                                 | 数学 贪心 | 需要能观察出规律，或者数学推导，否则需动归              |
| 面试题26      | 中等 | [树的子结构](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof)                                         | 树        | 二叉树版的字符串比对，时间复杂度O(M*N)可以了            |
| 面试题27      | 简单 | [二叉树的镜像](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof)                                | 树        | 递归 left, right = mirror(right), mirror[left]          |
| 面试题33      | 中等 | [二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof) | 树        | 翻转后序遍历结果就是镜像先序遍历+搜索树先序遍历递增性质 |
| 面试题40      | 简单 | [最小的k个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof)                                      | 排序 TopK | 堆排序（O(nlogk)） / 快速排序变种（O(n)）               |
| 面试题46      | 中等 | [把数字翻译成字符串](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof)                |           |                                                         |
| 面试题57 - II | 简单 | [和为s的连续正数序列](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof)              |           |                                                         |
| 面试题59 - II | 中等 | [队列的最大值](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof)                                   |           |                                                         |
| 面试题62      | 简单 | [圆圈中最后剩下的数字](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)    | 数学      | 约瑟夫环循环链表可解 但数学推导从结果反推起始位置更好   |

## LeetCode 周赛

| 周  | 序号 | 难度 | 题目                                                                                                               | 标签         | 思路                                       |
| --- | ---- | ---- | ------------------------------------------------------------------------------------------------------------------ | ------------ | ------------------------------------------ |
| 178 | 1365 | 简单 | [有多少小于当前数字的数字](https://leetcode-cn.com/problems/how-many-numbers-are-smaller-than-the-current-number/) | 数组         | 暴力 / 桶排序 / O(NlogN)排序               |
| 178 | 1366 | 中等 | [通过投票对团队排名](https://leetcode-cn.com/problems/rank-teams-by-votes)                                         | 排序         | 自定义排序的比较规则，哈希表存储信息       |
| 180 | 1380 | 简单 | [矩阵中的幸运数](https://leetcode-cn.com/problems/lucky-numbers-in-a-matrix/)                                      | 数组         | 统计每行最小与每列最大，取交集             |
| 180 | 1381 | 中等 | [设计一个支持增量操作的栈](https://leetcode-cn.com/problems/design-a-stack-with-increment-operation/)              | 数组 栈 设计 | 优化：可以设置一个增量数组用于弹出时再加上 |
| 182 | 5368 | 简单 | [找出数组中的幸运数](https://leetcode-cn.com/problems/find-lucky-integer-in-an-array/)                             | 数组         | 哈希表                                     |
| 182 | 5369 | 中等 | [统计作战单位数](https://leetcode-cn.com/problems/count-number-of-teams/)                                          | 数组         | 滑动窗口，先选最高和最低，再在中间选中间   |
| 182 | 5370 | 中等 | [设计地铁系统](https://leetcode-cn.com/problems/design-underground-system/)                                        | 设计         | 使用哈希表设计好信息存储即可               |

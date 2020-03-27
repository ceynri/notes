---
title: "LeetCode 题解速览"
date: "2020-03-27"
---

# LeetCode 题解速览

对于写过的题，将其最精华的思想浓缩为一句 key，组成 key list，以最后复习时过一遍这些思想。

> **⚠ 整理中**
> 
> 手动整理太慢
> 
> 预计编写一个脚本自动处理生成已经做过的题目及其相关信息的md表格

| 序号 | 难度   | 题目                                                                                                         | 标签          | 思路                                                 |
| ---- | ------ | ------------------------------------------------------------------------------------------------------------ | ------------- | ---------------------------------------------------- |
| 1    | 简单   | [两数之和](https://leetcode-cn.com/problems/two-sum/)                                                        | 数组          | 哈希表 利用key，使key+value=target                   |
| 2    | 中等   | [两数相加](https://leetcode-cn.com/problems/add-two-numbers/)                                                | 链表 加法模拟 | 进位状态 3while循环                                  |
| 11   | 中等   | [盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/)                                | 数组 贪心     | 短板决定高度 两板中较短一版向中心找更长的板          |
| 21   | 太简单 | [合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)                                 | 链表          | 两两比较 较长的链表的剩余部分直接接上                |
| ...  |        |                                                                                                              |               |                                                      |
| 94   | 中等   | [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)                          | 树            | 左遍历压栈到底，弹出节点值，取其右节点继续左遍历     |
| 100  | 太简单 | [相同的树](https://leetcode-cn.com/problems/same-tree/)                                                      | 树            | 选一种遍历方式同时遍历两棵树即可                     |
| 144  | 中等   | [二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)                         | 树            | 取节点值，右树压栈，往左树探                         |
| 235  | 简单   | [二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) | 二叉搜索树    | 利用搜索树性质，找到值在两数之间的数即可             |
| 404  | 简单   | [左叶子之和](https://leetcode-cn.com/problems/sum-of-left-leaves/)                                           | 树            | 给函数增加一个“当前节点是否为左节点”的标记           |
| 501  | 简单   | [二叉搜索树中的众数](https://leetcode-cn.com/problems/find-mode-in-binary-search-tree/)                      | 二叉搜索树    | 利用“中序遍历BST可得到递增数组”的性质                |
| 513  | 中等   | [找树左下角的值](https://leetcode-cn.com/problems/find-bottom-left-tree-value/)                              | 树            | 记录当前遍历的深度，最深的最左叶子总是会第一个遍历到 |

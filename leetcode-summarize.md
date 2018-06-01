# LeetCode 问题分类总结

## 数组中的问题

+ 二分查找法以及相关的操作：递归实现和非递归实现，floor 和 ceiling，《剑指Offer》上面关于二分查找法的应用
+ Move Zeros（第 283 题）
+ 第 27 题，删除元素
+ 第 26 题，数组元素去重
+ 第 80 题：最多保留两个
+ LeetCode 第 75 题
+ LeetCode 第 88 题，其实就是归并排序
+ LeetCode 第 215 题 leetcode-215-Kth-Largest-Element-in-an-Array。
+ 关于指针对撞的练习：例题1：LeetCode 第 167 题
练习1：Leetcode 第 125 题
练习2：Leetcode 第 344 题
练习3：Leetcode 第 345 题
练习4：Leetcode 第 11 题
+ 滑动窗口

## 查找表相关的问题

+ 第 LeetCode 第 349 题 计算两个数组的交集
+ 第 LeetCode 第 350 题 计算两个排序数组的交集
+ LeetCode 第 242 题 Valid Anagram
+ LeetCode 第 202 题 快乐数
+ LeetCode 第 290 题 Word Pattern
+ LeetCode 第 205 题 Isomorphic Strings 判断是否同构
+ 练习5：LeetCode 第 451 题 Sort Characters By Frequency
+ 例题1：LeetCode 第 1 题
+ 练习1：LeetCode 第 15 题 3Sum
+ LeetCode 第 18 题 4Sum
+ LeetCode 第 16 题 3Sum Closest
+ 例题1：LeetCode 第 454 题 4 个数之和
+ 练习1：LeetCode 第 49 题
+ 例题1：LeetCode 第 477 题（选错题了）位运算

+ LeetCode 第 447 题
+ LeetCode 第 149 题
+ 查找表和滑动窗口：LeetCode 第 219 题
+ 练习1：LeetCode 第 217 题
+ 例题1：LeetCode 第 220 题


## 链表

+ 链表问题只要涉及到头结点的操作的，一般都会用到设置虚拟头结点这个技巧；

+ 反转一个链表（206）、反转链表的指定部分（92）；
+ 83 题
+ 86 题
+ 328 题。奇数（Odd）偶数（Even）链表。奇数、偶数整理链表、partition 整理链表的一般思路：分别拿两个头结点，最后拼在一起；
+ LeetCode 第 2 题。两个数相加。两个存在链表中的数相加的问题；
+ LeetCode 第 445 题。两个数相加。
+ 删除节点：例题1：LeetCode 第 203 题。可以递归删除，或者穿针引线。
+ 练习1：LeetCode 第 82 题。给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 没有重复出现 的数字。
+ 归并两个有序的链表，还是穿针引线的问题；
+ 归并多个有序链表（多路归并排序），要用到优先队列
+ 例题1：LeetCode 第 24 题。两两交换链表中的节点。解法1：指针的交换。解法2：递归写法。
+ LeetCode 第 25 题。k个一组翻转链表。
+ LeetCode 第 147 题。
+ LeetCode 第 148 题。
+ 例题1：LeetCode 第 237 题。请编写一个函数，使其可以删除某个链表中给定的（非末尾的）节点，您将只被给予要求被删除的节点。
+ 链表与双指针：例题1：LeetCode 第 19 题。
+ LeetCode 第 61 题。
+ LeetCode 第 143 题。
+ LeetCode 第 234 题。


## 使用栈和队列完成的练习

+ LeetCode 上第 20 题：典型应用，检查括号匹配，是文本编辑器常见的一个功能
+ 练习1：LeetCode 第 150 题。逆波兰表达式求值。
+ LeetCode 第 71 题 简化路径
+ 栈和递归密不可分：分别可以解决二叉树的前序遍历、中序遍历、后序遍历 LeetCode 第144 题、练习2：LeetCode 第94 题、LeetCode 第145 题
+ 第 341 题：类的设计问题，挺有意思的
+ （有点意思）二叉树的层次遍历 102 题和 107 题，自底向上的层序遍历。

+ 103 二叉树的最大深度，实在太简单了，只有 3 行代码
+ 有点意思。考查的是层序遍历。LeetCode 第 199 题，二叉树从右边看，得到的一个数组。
+ （典型的问题，有多种解法）例题1：LeetCode 第 279 题（油管缺少下载）
+ （花了我非常多的时间，一定要重视起来）LeetCode 第 127 题（较简单）、LeetCode 第 126 题（难）
+ LeetCode 第 347 题：前 K 个高频元素
+ （基础、典型、必会）23. 合并K个排序链表（1、优先队列；2、分治归并）


## 二叉树相关的问题
+ 二叉树的最大深度和最小深度（第 104 和 第 111 题（差一张图））
+ 反转一棵二叉树（第 226 题），为什么中序遍历不能胜任。
+ 判断两个二叉树是否一样（LeetCode 第 100 题）
+ 检查一棵树是否是镜像对称的（第 101 题），解法很多，LeetCode 第 101 题（典型问题）
+ 给出一个完全二叉树，求出该树的节点个数。LeetCode 第 222 题 
+ 判断是否是平衡二叉树（使用后序遍历，第 110 题）LeetCode 第 110 题
+ LeetCode 第 112 题Path Sum
+ LeetCode 第 111 题（回顾）

+（完成）练习2：LeetCode 第 404 题（油管视频缺少下载）
LeetCode 第 257 题。题目要求：得到二叉树的所有路径。
第 113 题。题目要求：给定一棵二叉树，返回所有从根节点到叶子节点的路径，并且要等于指定的和。
+ 第 129 题。题目要求：给定一棵二叉树，每个节点只包含数字 0-9，从根节点到叶子节点的每条路径可以表示成一个数，求这些数的和。

+ LeetCode 第 437 题
+ 235. 二叉搜索树的最近公共祖先，简单，但是二叉树的最近公共祖先就没有那么容易了
+ LeetCode 第 98 题 是否是二分搜索树
+ （一定要会！）LeetCode 第 450 题 450. 删除二叉搜索树中的节点

+ LeetCode 第 108 题 将有序数组转换为二叉搜索树
+ （基础、重要、建议重做）LeetCode 第 230 题：二叉搜索树中第 K 小的元素（我的解法比《剑指Offer》的要简单，不要被这本书带偏了）
+ LeetCode 第 236 题 二叉树的最近公共祖先《剑指Offer》也有这题
+ 序列化二叉树和反序列化二叉树（《剑指 Offer 》第 37 题）
+ 序列化一棵二叉树、反序列化一棵二叉树，
+ 使用前序遍历和中序遍历的结果还原一棵二叉树
+ 二叉树的最小深度（第 111 题）：虽然是简单题，但是有比较容易忽视的一个特例


## 回溯问题

+ 电话号码的字母组合 17
+ LeetCode 第 93 题 给定一个只包含数字的字符串，复原它并返回所有可能的 IP 地址格式。
+ LeetCode 第 131 题。分割回文串。给定一个字符串 s，将 s 分割成一些子串，使每个子串都是回文串。返回 s 所有可能的分割方案。
+ LeetCode 第 46 题。给定一个没有重复数字的序列，返回其所有可能的全排列。

+ （重要，可优化）LeetCode 第 47 题。给定一个可包含重复数字的序列，返回所有不重复的全排列。按顺序查找，已经用过的数字就不会再使用，因此不用设置 used 数组。

+ 例题1：LeetCode 第 77 题，给定两个整数 n 和 k，返回 1 ... n 中所有可能的 k 个数的组合。
+ LeetCode 第 39 题。给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

+ 练习2：LeetCode 第 40 题，还是组合问题。
+ LeetCode 第 216 题。找出所有相加之和为 n 的 k 个数的组合。组合中只允许含有1 - 9的正整数，并且每种组合中不存在重复的数字。
+ 排列问题 第 46 题（赶快整理）
+ LeetCode 第 78 题。给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。
+ LeetCode 第 90 题：给定一个可能包含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。说明：解集不能包含重复的子集。
+ LeetCode 第 401 题：二进制手表问题。
+ 例题1：LeetCode 第 79 题 79. 单词搜索
LeetCode 第 80 题，给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素最多出现两次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

+ LeetCode 第 200 题：200. 岛屿的个数
+ 130,被围绕的区域,
+ 417. Pacific Atlantic Water Flow 
+ n 皇后问题 第 51 题，第 52 题 
+ 数独问题 第 37 题
+ 

## 动态规划

+ 斐波拉契数列
+ LeetCode 第 70 题 Climbing Stairs
+ 练习1：LeetCode 第 120 题 Triangle
+ 第 64 题 Minimum Path Sum 最小路径和
+ 例题1：LeetCode 第 343 题 Integer Break
+ LeetCode 第 279 题，求一个正整数能分解成完全平方数之和的最少个数。
+ （非常重要的 dp 问题）练习2：LeetCode 第 91 题 Decode Ways
+ （简单，可以从空间复杂度优化）练习3：LeetCode 第 62 题 Unique Paths
+ LeetCode 第 63 题 Unique Paths II
+ 打家劫舍系列：例题1：LeetCode 第 198 题、练习1：LeetCode 第 213 题 House Robber II、LeetCode 第 337 题 House Robber III
+ （状态机解决）练习3：LeetCode 第 309 题 Best Time to Buy and Sell Stock with Cooldown
+ 背包问题—— Knapsack01（6题）
+ LeetCode 第 416 题 Partition Equal Subset Sum
+ （重要，建议重刷，思考它和整数分解的关系，还要注意一些细节）练习1：LeetCode 第 322 题 Coin Change，看看哪里用到了“滚动数组”的技巧，典型的一维动态规划问题
+ （重要，重刷，对这道问题的理解还不够深刻）练习2：LeetCode 第 377 题 Combination Sum IV
+ LeetCode 第 474 题 Ones and Zeroes
+ LeetCode 第 139 题 Word Break（这个问题被很多大公司采用，望留意）
+ LeetCode 第 494 题 Target Sum
+ 例题1：LeetCode 第 300 题 Longest Increasing Subsequence
+ 练习1：LeetCode 第 376 题 Wiggle Subsequence
+ 最长公共子序列问题（Longest Common Sequence）


## 贪心算法

+ LeetCode 第 435 题 

## 高级数据结构

### 线段树

### 单词查找树 Trie

+ LeetCode 第 208 题 Implement Trie (Prefix Tree)
+ LeetCode 第 211 题 Add and Search Word - Data structure design
+ LeetCode 第 677 题 Map Sum Pairs
+ 745. 前缀和后缀搜索 https://leetcode-cn.com/problems/prefix-and-suffix-search/description/
+ 720. 词典中最长的单词 https://leetcode-cn.com/problems/longest-word-in-dictionary/description/

## 其它技巧

### 滚动数组（节约空间）

### 使用状态机画图求解


### 位运算帮上的大忙





# Maximum Depth of Binary Tree

## 题目描述和难度
+ 题目描述：给定一个二叉树，找出其最大深度。二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。说明: 叶子节点是指没有子节点的节点。
+ 题目难度：简单。
+ 英文网址：[104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)  。
+ 中文网址：[104. 二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/description/)  。
## 思路分析
求解关键：二叉树的问题可以考虑使用递归方法来完成。但如果这道题要求最小深度，那就有点不一样了，请参考 LeetCode 第 111 题。
## 参考解答
### 参考解答1

```java
public class Solution {

    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
    
}
```
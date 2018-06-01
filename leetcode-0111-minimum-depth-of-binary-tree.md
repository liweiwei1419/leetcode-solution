# 111. Minimum Depth of Binary Tree

## 题目描述和难度
+ 题目描述：给定一个二叉树，找出其最小深度。最小深度是从根节点到最近叶子节点的最短路径上的节点数量。说明: 叶子节点是指没有子节点的节点。
+ 题目难度：简单。
+ 英文网址：[111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/description/)  。
+ 中文网址：[111. 二叉树的最小深度](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/description/)  。
## 思路分析
求解关键：不要简单地认为这道题和“求二叉树的最大深度”（LeetCode 第 104 题）一样，要考虑到“左子树和右子树其中之一为空”这种特殊情况。

## 参考解答
### 参考解答1

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode(int x) {
        val = x;
    }
}

public class Solution {

    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        // 这一步要特别注意，是一个很容易被忽略的情况
        if (root.left == null || root.right == null) {
            return Integer.max(minDepth(root.left), minDepth(root.right)) + 1;

        }
        return Integer.min(minDepth(root.left), minDepth(root.right)) + 1;
    }
}
```
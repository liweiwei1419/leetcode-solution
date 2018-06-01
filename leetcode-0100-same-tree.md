# Same Tree

## 题目描述和难度
+ 题目描述：给定两个二叉树，编写一个函数来检验它们是否相同。如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。
+ 题目难度：简单。
+ 英文网址：[100. Same Tree](https://leetcode.com/problems/same-tree/description/)  。
+ 中文网址：[100. 相同的树](https://leetcode-cn.com/problems/same-tree/description/)  。
## 思路分析
求解关键：非常简答的一个问题，几乎不加思索就可以完成，注意讨论结点是否为空的特殊情况就好了。

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
    public boolean isSameTree(TreeNode p, TreeNode q) {
        // 先处理最特殊的情况，都为空结点的时候
        if (p == null && q == null) {
            return true;
        }
        // 走到这里说明两个结点都同时不为空，那么其中之一为空，或者两个结点的值不相等的时候，返回 false
        if (p == null || q == null || p.val != q.val) {
            return false;
        }
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}
```

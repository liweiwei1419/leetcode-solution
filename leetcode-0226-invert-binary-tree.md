# Invert Binary Tree

## 题目描述和难度
+ 题目描述：翻转一棵二叉树。
+ 题目难度：简单。
+ 英文网址：[226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/description/)  。
+ 中文网址：[226. 翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/description/)  。
## 思路分析
求解关键：这道问题可以说是一个经典的问题。LeetCode 上有如下备注：

> 这个问题是受到 Max Howell 的 原问题 启发的 ：

> 谷歌：我们90％的工程师使用您编写的软件(Homebrew)，但是您却无法在面试时在白板上写出翻转二叉树这道题，这太糟糕了。


思路1：我们可以使用递归方法来完成，我们写好之后，会发现其实就是完成了一次深度优先遍历，并且是前序遍历，有的朋友可能写出来的后序遍历，那么我们不禁要问，中序遍历可不可以，答案是不可以，因为中序遍历很可能一个结点会被翻转两次，这与我们的要求是违背的。

<img src="https://liweiwei1419.github.io/images/leetcode-solution/226-1.jpg" width="600">

那么广度优先遍历可以吗？事实上是可以的，这也就是我们的非递归的解决方案。
思路2：如果不让我们用递归，我们完全可以按照递归的思路模拟递归完成。

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

    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }
        // 左子树和右子树交换，即使左右子树都空也不影响正确性
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
        // 递归翻转左右子树
        invertTree(root.left);
        invertTree(root.right);
        return root;
    }
}
```


### 参考解答2
```java
import java.util.LinkedList;

public class Solution2 {

    public TreeNode invertTree(TreeNode root) {
        // 结点为空的特殊情况要先考虑
        if (root == null) {
            return null;
        }
        LinkedList<TreeNode> queue = new LinkedList<>();
        queue.addLast(root);
        while (!queue.isEmpty()) {
            TreeNode curNode = queue.removeFirst();
            // 只要其中之一非空，我都交换，并且把非空的添加到队列里
            if (curNode.left != null || curNode.right != null) {
                // 先翻转
                TreeNode temp = curNode.left;
                curNode.left = curNode.right;
                curNode.right = temp;
                // 把非空的节点加入队列
                if (curNode.left != null) {
                    queue.addLast(curNode.left);
                }
                if (curNode.right != null) {
                    queue.addLast(curNode.right);
                }
            }
        }
        return root;
    }
}
```
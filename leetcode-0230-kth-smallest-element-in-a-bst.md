# Kth Smallest Element in a BST

## 题目描述和难度
+ 题目描述：给定一个二叉搜索树，编写一个函数 kthSmallest 来查找其中第 k 个最小的元素。
+ 题目难度：中等。
+ 英文网址：[230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/)  。
+ 中文网址：[230. 二叉搜索树中第K小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/description/)  。
## 思路分析
求解关键：1、二分搜索树的顺序性；2、二叉树中序遍历，特别地，二分搜索树的中序遍历得到的是一个有序数组。

+ 简而言之就是在中序遍历的时候数个数，第 1 个遍历到的是第 1 个最小的元素，第 2 个遍历到的是第 2 个最小的元素，数到第 k 个够数了，就不用再遍历了。

## 参考解答
### 参考解答1

注意：这里一定要把计数的变量设置成“成员变量”，如果设置成局部变量，使得 k 作为参数在方法中传递，就变成了值传递，就得不到正确的结果。

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode(int x) {
        val = x;
    }
}

// 解题关键：中序遍历
public class Solution {

    private int res;
    private int count;

    // k 如果在方法传递的过程中是值传递，所以把它设置为成员变量，这样就是引用传递
    // 因为我们要用到 k 全局的值，去数出，我是第几个中序遍历到的值
    public int kthSmallest(TreeNode root, int k) {
        count = k;
        inOrder(root);
        return res;
    }

    private void inOrder(TreeNode node) {
        if (node == null) {
            return;
        }
        inOrder(node.left);
        count--;
        if (count == 0) {
            res = node.val;
            return;
        }
        inOrder(node.right);
    }
}
```
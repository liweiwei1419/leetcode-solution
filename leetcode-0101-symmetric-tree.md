# Symmetric Tree

## 题目描述和难度
+ 题目描述：给定一个二叉树，检查它是否是镜像对称的。
+ 题目难度：简单。
+ 英文网址：[101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/)  。
+ 中文网址：[101. 对称二叉树](https://leetcode-cn.com/problems/symmetric-tree/description/)  。
## 思路分析
求解关键：

+ 思路1（对应参考解答1）：先拷贝一棵二叉树，再反转，将反转以后的二叉树和自己比较，看看是否相等，这个思路就转化成了以前我们解决过的问题。另外复制的时候，我们可以反着复制，然后比较。
+ 思路2（对应参考解答2）：设置一个辅助函数，递归去判断两棵子树是否镜面对称。
+ 思路3（对应参考解答3）：使用队列，并且是双端队列（链表实现）这个辅助数据结构。画出出队入队的顺序，就很清楚了。

<img src="https://liweiwei1419.github.io/images/leetcode-solution/101-1.jpg" width="600">

## 参考解答
### 参考解答1

说明：注意下面的 `copyBinaryTree` 方法。

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
    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        TreeNode copyBinaryTree = copyBinaryTree(root);
        TreeNode invertBinaryTree = invertBinaryTree(copyBinaryTree);
        return isSameTree(root, invertBinaryTree);
    }

    private boolean isSameTree(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) {
            return true;
        }
        if (t1 == null || t2 == null || t1.val != t2.val) {
            return false;
        }
        return isSameTree(t1.left, t2.left) && isSameTree(t1.right, t2.right);
    }

    private TreeNode invertBinaryTree(TreeNode node) {
        if (node == null) {
            return node;
        }
        invertBinaryTree(node.left);
        invertBinaryTree(node.right);
        TreeNode temp = node.left;
        node.left = node.right;
        node.right = temp;
        return node;
    }

    // 也使用递归的方式完成（熟悉一下如何完成二叉树的复制）
    private TreeNode copyBinaryTree(TreeNode node) {
        if (node == null) {
            return null;
        }
        TreeNode newTreeNode = new TreeNode(node.val);
        newTreeNode.left = copyBinaryTree(node.left);
        newTreeNode.right = copyBinaryTree(node.right);
        return newTreeNode;
    }
}
```

### 参考解答2（推荐）

```java
public class Solution {

    // 画出 4 层结构图就容易发现递归关系了
    private boolean isSymmetric(TreeNode p1, TreeNode p2) {
        // 左右都为空，判为相等
        if (p1 == null && p2 == null) {
            return true;
        }
        // 走到这里左右之一至少非空，或者都非空，但它们的 val 不等，都不能叫做 symmetric tree
        if (p1 == null || p2 == null || p1.val != p2.val) {
            return false;
        }
        // 对称地去比较，p1 的左边和 p2 的右边
        // p1 的右边和 p2 的左边
        return isSymmetric(p1.left, p2.right) && isSymmetric(p1.right, p2.left);
    }

    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        return isSymmetric(root.left, root.right);
    }
}
```

### 参考解答3

参考资料：

```java
import java.util.LinkedList;

// https://leetcode-cn.com/problems/symmetric-tree/description/
public class Solution3 {

    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        LinkedList<TreeNode> linkedList = new LinkedList<>();
        linkedList.addFirst(root.left);
        linkedList.addLast(root.right);
        while (!linkedList.isEmpty()) {
            // 出队的时候，看看是否有左右孩子，分别入队
            TreeNode lNode = linkedList.removeFirst();
            TreeNode rNode = linkedList.removeLast();
            if (lNode == null && rNode == null) {
                continue;
            }
            if (lNode == null || rNode == null) {
                return false;
            }
            linkedList.addFirst(lNode.right);
            linkedList.addFirst(lNode.left);
            linkedList.addLast(rNode.left);
            linkedList.addLast(rNode.right);

            if (lNode.val != rNode.val) {
                return false;
            }
        }
        return true;
    }
}
```



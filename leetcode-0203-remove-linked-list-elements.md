# 填写

## 题目描述和难度
+ 题目描述：删除链表中等于给定值 val 的所有节点。
+ 题目难度：简单。
+ 英文网址：[203. Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/description/)  。
+ 中文网址：[203. 删除链表中的节点](https://leetcode-cn.com/problems/remove-linked-list-elements/description/)  。
## 思路分析
求解关键：常规解法画图分析指针的指向，看图直接写出代码，这是思路1。

思路1：删除节点这件事情很可能发生在链表的头结点，因此需要对头结点特殊处理。常用的处理头结点的技巧是设立虚拟头结点，这样头结点的处理逻辑和非头结点就可以统一起来。

思路2：使用递归删除，这样就不用处理“穿针引线”的问题了。步骤：（1）处理最简单的情况。（2）假设规模小的情况解决了，大一级（多 1 个元素）的情况的如何与之产生联系。

补充说明：对于单链表的程序的测试，建议给 `ListNode` 类添加可以传入数组的构造方法，并覆盖 `toString()` 方法方便检测我们编写的程序正确与否。

## 参考解答
### 参考解答1：常规解法，穿针引线

```java
// Definition for singly-linked list.
class ListNode {

    int val;
    ListNode next;

    ListNode(int x) {
        val = x;
    }

    // 下面，我们将 LeetCode 中的给出的链表的节点这个类进行一些扩展，方便我们的调试
    // 1、给出一个数字数组，通过数组构建数字链表
    public ListNode(int[] arr) {
        if (arr == null || arr.length == 0) {
            throw new IllegalArgumentException("arr can not be empty");
        }
        // 体会这里 this 指代了什么，其实就是 head
        // 因为这是一个构造函数，所以也无须将 head 返回
        this.val = arr[0];
        ListNode cur = this;
        for (int i = 1; i < arr.length; i++) {
            cur.next = new ListNode(arr[i]);
            cur = cur.next;
        }
    }

    // 2、重写 toString() 方法，方便我们查看链表中的元素
    @Override
    public String toString() {
        StringBuilder s = new StringBuilder();
        ListNode cur = this; // 还是要特别注意的是，理解这里 this 的用法
        while (cur != null) {
            s.append(cur.val + " -> ");
            cur = cur.next;
        }
        s.append("NULL");
        return s.toString();
    }
}

public class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummyNode = new ListNode(-1);
        dummyNode.next = head;
        ListNode cur = dummyNode;
        ListNode next;
        while (cur.next != null) {
            if (cur.next.val == val) {
                next = cur.next;
                cur.next = next.next;
                next.next = null;
            } else {
                cur = cur.next;
            }
        }
        return dummyNode.next;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 6, 3, 4, 5, 6};
        ListNode head = new ListNode(nums);
        int val = 6;
        Solution solution = new Solution();
        ListNode removeElements = solution.removeElements(head, val);
        System.out.println(removeElements);
    }
}
```
### 参考解答2：使用递归方法（个人推荐，因为不用穿针引线，代码也很简洁）

```java
class Solution2 {

    // 这是一个递归方法，首先处理递归到底的情况
    public ListNode removeElements(ListNode head, int val) {
        // 首先处理递归到底的情况
        if (head == null) {
            return head;
        }
        // 把一个问题转化为规模更小的问题
        ListNode res = removeElements(head.next, val);
        // 下面处理原始规模的问题如何与小规模的问题建立联系
        if (head.val == val) {
            // 当前这个节点必须要被删掉
            return res;
        } else {
            head.next = res;
            return head;
        }
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 6, 3, 4, 5, 6};
        ListNode head = new ListNode(nums);
        int val = 6;
        Solution solution = new Solution();
        ListNode removeElements = solution.removeElements(head, val);
        System.out.println(removeElements);
    }
}
```

说明：更简洁的一种写法。

```java
public class Solution3 {

    public ListNode removeElements(ListNode head, int val) {
        if (head == null) {
            return head;
        }
        head.next = removeElements(head.next, val);
        return head.val == val ? head.next : head;
    }
}
```
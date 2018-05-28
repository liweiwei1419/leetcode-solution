# reverse-linked-list-ii

## 题目描述和难度
+ 题目描述：
+ 题目难度：简单。中等。困难
+ 英文网址：[92. Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/description/)  。
+ 中文网址：[92. 反转链表 II](https://leetcode-cn.com/problems/reverse-linked-list-ii/description/)  。
## 思路分析
求解关键：

<img src="https://liweiwei1419.github.io/images/leetcode-solution/92-1.jpg" width="500">

<img src="https://liweiwei1419.github.io/images/leetcode-solution/92-2.jpg" width="500">

1. 反转链表指定的部分，用到了“设置虚拟头结点”这个技巧，只要涉及到头节点的前一个节点的操作，一般都会用到虚拟头结点这个技巧，使得我们的代码更加简洁，一定要注意，返回的时候，要返回虚拟头结点的 next 指针指向的那个元素。
2. 关注临界值，`pre` 要循环几次，链表要“滚”几轮，都是这里要关注的点，因此代入一些具体值就能避免出错，正确的结果无非就是我们以为的那个数字 +1 或者 -1；
3. 自己在纸上画出图来，验证一下两轮以后代码是不是得到我们想要的一致结果；
4. 关于代码：每“滚”一次，其实 `cur` 的指针都不变，`pre` 也不变，`next` 变化，但是一直跟在 `cur` 的后面，所以它的位置在循环开始的时候确定。每次 `cur` 的 `next` 都会移到 `pre` 的 `next`，这就是循环体内第 2 行代码的含义；
5. 为了便于测试，我通常会给 `ListNode` 增加两个静态方法：（1）通过一个数组创建链表 `createListNode`；（2）打印一个链表 `printLinkedList`。

## 参考解答

### 参考解答1

```java
class ListNode {
    int val;
    ListNode next;

    ListNode(int x) {
        val = x;
    }

    public static ListNode createListNode(int[] nums) {
        if (nums.length == 0) {
            return null;
        }
        ListNode head = new ListNode(nums[0]);
        ListNode curr = head;
        for (int i = 1; i < nums.length; i++) {
            curr.next = new ListNode(nums[i]);
            curr = curr.next;
        }
        return head;
    }

    public static void printLinkedList(ListNode head) {
        ListNode cur = head;
        while (cur != null) {
            System.out.print(cur.val + " -> ");
            cur = cur.next;
        }
        System.out.println("NULL");
    }
}

public class Solution {

    public ListNode reverseBetween(ListNode head, int m, int n) {
        // 设置 dummyNode 是这一类问题的一般做法
        ListNode dummyNode = new ListNode(-1);
        dummyNode.next = head;
        ListNode pre = dummyNode;
        for (int i = 0; i < m - 1; i++) {
            pre = pre.next;
        }
        ListNode cur = pre.next;
        ListNode next;
        for (int i = 0; i < n - m; i++) {
            next = cur.next;
            cur.next = next.next;
            next.next = pre.next;
            pre.next = next;
        }
        return dummyNode.next;
    }

    public static void main(String[] args) {
        int[] nums = new int[]{1, 2, 3, 4, 5};
        ListNode head = ListNode.createListNode(nums);
        ListNode.printLinkedList(head);
        System.out.println("反转之后");
        ListNode newListNode = new Solution().reverseBetween(head, 2, 4);
        ListNode.printLinkedList(newListNode);
    }
}
```

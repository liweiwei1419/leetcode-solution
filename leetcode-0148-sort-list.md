# 148. Sort List

## 题目描述和难度
+ 题目描述：在 O(n log n) 时间复杂度和常数级空间复杂度下，对链表进行排序。
+ 题目难度：中等。
+ 英文网址：[148. Sort List](https://leetcode.com/problems/sort-list/description/)  。
+ 中文网址：[148. 排序链表](https://leetcode-cn.com/problems/sort-list/description/)  。
## 思路分析
求解关键：

由顶至底的归并排序是待排序的子数组越来越小的过程，而由底至顶的归并排序是待归并的子数组越来越大的过程。
+ 看成每个单结点都是排好序的单链表，这样就可以使用分治的思想来完成，或者把它们都放入优先队列。
一个宝贵的经验就是：维护两个指针，一快一慢。快指针每次后移两个单位，慢指针每次只移动一个单位。当快指针移动到tail或者最后一个有效节点时，慢指针就指向了中间的节点。

## 参考解答
### 参考解答1

```java
class ListNode {
    int val;
    ListNode next;

    ListNode(int x) {
        val = x;
    }

    ListNode(int[] nums) {
        ListNode currNode = this;
        currNode.val = nums[0];
        for (int i = 1; i < nums.length; i++) {
            currNode.next = new ListNode(nums[i]);
            currNode = currNode.next;
        }
    }

    @Override
    public String toString() {
        ListNode currNode = this;
        StringBuilder s = new StringBuilder();
        while (currNode != null) {
            s.append(currNode.val);
            s.append(" -> ");
            currNode = currNode.next;
        }
        s.append("NULL");
        return s.toString();
    }
}

public class Solution {

    public ListNode sortList(ListNode head) {
        // 递归终止的条件，即满足下面条件就不用找中点，可以直接返回
        if (head == null || head.next == null) {
            return head;
        }
        // 使用归并排序、分治思想，先要找到链表的中间结点
        ListNode fast = head;
        ListNode slow = head;
        // 下面这段代码是找链表中间结点的一般做法
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        // 定义位于中间结点的下一个结点，从它那里将一个链表切开
        ListNode midNext = slow.next;
        // 这里一定要记得从中间切开，分割成两个链表
        slow.next = null;
        ListNode listNodeLeft = sortList(head);
        ListNode listNodeRight = sortList(midNext);
        // 合并两个已经排序的单链表，这是我们很熟悉的操作了
        return mergeOfTwoSortListNode(listNodeLeft, listNodeRight);
    }

    private ListNode mergeOfTwoSortListNode(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }
        if (l1.val < l2.val) {
            l1.next = mergeOfTwoSortListNode(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeOfTwoSortListNode(l1, l2.next);
            return l2;
        }
    }

    public static void main(String[] args) {
        int[] nums = new int[]{4, 2, 1, 3};
        ListNode head = new ListNode(nums);
        Solution solution = new Solution();
        ListNode sortList = solution.sortList(head);
        System.out.println(sortList);
    }
}
```
# remove-duplicates-from-sorted-list

## 题目描述和难度
+ 题目描述：给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。
+ 题目难度：简单。
+ 英文网址：[83. Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/description/)  。
+ 中文网址：[83. 删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/description/)  。
## 思路分析
求解关键：画图。

+ 只要画出分析的图，代码的实现就是水到渠成的事情了。

<img src="https://liweiwei1419.github.io/images/leetcode-solution/83-1.jpg" width="600">

1. 空的情况不要忘记写在最开始，最简单的情况最容易忽略；  
2. 这里不会涉及头结点的前一个节点的操作，因此不需要设立虚拟的头结点；  
3. 删除链表中的节点的固定的套路是 `while(cur.next!=null)`，即去判断当前节点的下一个节点是不是我们要删除的节点，如果是，则当前节点的下一个节点的指向跳过它，所以这里只要 `cur` 和 `next` 就可以了，不用 `pre`。

## 参考解答
### 参考解答1

```java
class ListNode {
    int val;
    ListNode next;

    ListNode(int x) {
        val = x;
    }

    public ListNode(int[] nums) {
        if (nums == null || nums.length == 0) {
            throw new IllegalArgumentException("arr can not be empty");
        }
        this.val = nums[0];
        ListNode curr = this;
        for (int i = 1; i < nums.length; i++) {
            curr.next = new ListNode(nums[i]);
            curr = curr.next;
        }
    }

    @Override
    public String toString() {
        StringBuilder s = new StringBuilder();
        ListNode cur = this;
        while (cur != null) {
            s.append(cur.val + " -> ");
            cur = cur.next;
        }
        s.append("NULL");
        return s.toString();
    }
}

public class Solution {

    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode cur = head;
        ListNode next;
        while (cur.next != null) {
            next = cur.next;
            if (next.val == cur.val) {
                cur.next = next.next;
                next.next = null;
            } else {
                cur = cur.next;
            }
        }
        return head;
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 2, 3, 3};
        ListNode head = new ListNode(nums);
        Solution solution = new Solution();
        System.out.println("删除排序链表中的重复元素以后：");
        ListNode deleteDuplicates = solution.deleteDuplicates(head);
        System.out.println(deleteDuplicates);
    }
}
```
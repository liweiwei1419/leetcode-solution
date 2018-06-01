# 21. Merge Two Sorted Lists

## 题目描述和难度
+ 题目描述：将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 
+ 题目难度：简单。
+ 英文网址：[21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/description/)  。
+ 中文网址：[21. 合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/description/)  。
## 思路分析
求解关键：画图可以很清晰地看出指针的指向，顺利地完成“穿针引线”的工作。

思路1：（对应参考解答1）穿针引线。

<img src="https://liweiwei1419.github.io/images/leetcode-solution/21-1.jpg" width="600">


<img src="https://liweiwei1419.github.io/images/leetcode-solution/21-2.jpg" width="600">


思路2：（对应参考解答2）如果不想“穿针引线”，让递归方法来处理是一个比较不错的选择，类似的练习还有 []()。

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

    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummyNode = new ListNode(-1);
        ListNode p1 = l1;
        ListNode p2 = l2;
        ListNode curNode = dummyNode;
        while (p1 != null && p2 != null) { // 两者都不为空的时候，才有必要进行比较
            if (p1.val < p2.val) {
                curNode.next = p1; // 指针修改发生在这里
                p1 = p1.next;
            } else {
                curNode.next = p2;// 指针修改发生在这里
                p2 = p2.next;
            }
            curNode = curNode.next;
        }
        // 跳出循环是因为 p1 == null 或者 p2 == null
        if (p1 == null) {
            curNode.next = p2;
        }
        if (p2 == null) {
            curNode.next = p1;
        }
        return dummyNode.next;
    }

    public static void main(String[] args) {
        int[] nums1 = {1, 3, 5, 7};
        int[] nums2 = {2, 4, 6};

        ListNode l1 = new ListNode(nums1);
        ListNode l2 = new ListNode(nums2);

        Solution solution = new Solution();
        ListNode mergeTwoLists = solution.mergeTwoLists(l1, l2);
        System.out.println(mergeTwoLists);
    }
}
```

### 参考解答2

```java
// 使用递归方法完成
public class Solution2 {

    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        // 先写递归终止的条件
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }
        // 假设规模小的问题已经解决，如何建立和原始规模问题之间的关系
        ListNode mergeNode;
        if (l1.val < l2.val) {
            mergeNode = l1; // l1 被选出，谁小谁在前面
            mergeNode.next = mergeTwoLists(l1.next, l2);
        } else {
            mergeNode = l2; // l2 被选出，谁小谁在前面
            mergeNode.next = mergeTwoLists(l1, l2.next);
        }
        return mergeNode;
    }
}
```
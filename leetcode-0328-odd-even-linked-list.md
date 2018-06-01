# Odd Even Linked List

## 题目描述和难度
+ 题目描述：给定一个单链表，把所有的奇数节点和偶数节点分别排在一起。请注意，这里的奇数节点和偶数节点指的是节点编号的奇偶性，而不是节点的值的奇偶性。请尝试使用**原地算法**完成。你的算法的空间复杂度应为 O(1)，时间复杂度应为 O(nodes)，nodes为节点总数。
+ 题目难度：中等。
+ 英文网址：[328. Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/description/)  。
+ 中文网址：[328. 奇偶链表](https://leetcode-cn.com/problems/odd-even-linked-list/description/)  。
## 思路分析
求解关键：题目要求**原地算法**完成，那么就一定得“穿针引线”了。
+ 思路1：可以使用 [LeetCode 第 86 题题解思路 2 ](https://liweiwei1419.github.io/leetcode-solution/leetcode-0086-partition-list/) 完成。  
+ 思路2：同样使用两个指针，一次跳过一个节点完成“穿针引线”，特别注意要一些边界情况的判断。

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
    public ListNode oddEvenList(ListNode head) {
        ListNode dummyNodeOdd = new ListNode(-1);
        ListNode dummyNodeEven = new ListNode(-1);
        ListNode curOdd = dummyNodeOdd;
        ListNode curEven = dummyNodeEven;
        int count = 0;
        while (head != null) {
            if (count % 2 == 0) {
                curOdd.next = head;
                curOdd = curOdd.next;
            } else {
                curEven.next = head;
                curEven = curEven.next;
            }
            head = head.next;
            count++;
        }
        curOdd.next = dummyNodeEven.next;
        // 特别注意：最后这一步不能忘记，否则会产生一个循环链表
        curEven.next = null;
        return dummyNodeOdd.next;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4, 5};
        ListNode head = new ListNode(nums);
        Solution solution = new Solution();
        ListNode oddEvenList = solution.oddEvenList(head);
        System.out.println(oddEvenList);
    }
}
```
### 参考解答2（推荐）
+ 注意1：我们采用一次跳过一个节点“穿针引线”的办法来完成这个问题；
+ 注意2：在 `while` 循环体中，如果结点个数是奇数的话，偶数索引的最后一个元素的 `next` 指针会指向一个 `null` （因为跳过一个结点改变 `next` 指针的操作是一起进行的），这一点完全可以分类讨论，因为就两种情况，如下图所示：

<img src="https://liweiwei1419.github.io/images/leetcode-solution/328-1.jpg" width="600">

```java
public class Solution2 {

    public ListNode oddEvenList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode oddHead = head;
        ListNode evenHead = head.next;

        ListNode oddCur = oddHead;
        ListNode evenCur = evenHead;
        // 执行循环的条件不能写错
        while (evenCur != null && evenCur.next != null) {
            oddCur.next = oddCur.next.next;
            evenCur.next = evenCur.next.next;

            oddCur = oddCur.next;
            evenCur = evenCur.next;
        }
        oddCur.next = evenHead;
        return oddHead;
    }
}
```
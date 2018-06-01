# Partition List

## 题目描述和难度
+ 题目描述：给定一个链表和一个特定值 x，对链表进行分隔，使得所有小于 x 的节点都在大于或等于 x 的节点之前。你应当保留两个分区中每个节点的初始相对位置。
+ 题目难度：中等。
+ 英文网址：[86. Partition List](https://leetcode.com/problems/partition-list/description/)  。
+ 中文网址：[86. 分隔链表](https://leetcode-cn.com/problems/partition-list/description/)  。
## 思路分析
求解关键：
其实就是我们在数组中的 partition 这个过程，在数组中，我们要通过不断地交换元素的位置来实现 partition 。对于这道问题，穿针引线可能有些麻烦，但是我们完全可以新建两个链表，最后把它们合并在一起，这是思路1；但是我们也完全可以穿针引线，只不过要设置两个头结点，最后把它们合在一起就可以了，省去了一直 new 节点的操作，这是思路2。

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

    public ListNode partition(ListNode head, int x) {
        ListNode dummyNodeL = new ListNode(-1); // 比 x 小的虚拟头结点
        ListNode dummyNodeR = new ListNode(-1); // 大于等于 x 的虚拟头结点
        ListNode curL = dummyNodeL; // 用于遍历
        ListNode curR = dummyNodeR; // 用于遍历
        int val;
        while (head != null) {
            val = head.val;
            if (val < x) { // 接在 L 的后面
                curL.next = new ListNode(val);
                curL = curL.next;
            } else { // 接在 R 的后面
                curR.next = new ListNode(val);
                curR = curR.next;
            }
            head = head.next;
        }
        curL.next = dummyNodeR.next; // 把较小的链表接在较大的链表后面
        return dummyNodeL.next;
    }

    public static void main(String[] args) {
        int[] nums = {1, 4, 3, 2, 5, 2};
        int x = 3;
        ListNode head = new ListNode(nums);
        Solution solution = new Solution();
        System.out.println("分隔链表之后：");
        ListNode partition = solution.partition(head, x);
        System.out.println(partition);
    }
}
```

### 参考解答2（推荐）

<img src="https://liweiwei1419.github.io/images/leetcode-solution/86-1.jpg" width="600">

```java
public class Solution2 {

    public ListNode partition(ListNode head, int x) {
        ListNode dummyNodeL = new ListNode(-1); // 比 x 小的虚拟头结点
        ListNode dummyNodeR = new ListNode(-1); // 大于等于 x 的虚拟头结点
        ListNode curL = dummyNodeL; // 用于遍历
        ListNode curR = dummyNodeR; // 用于遍历
        int val;
        while (head != null) {
            val = head.val;
            if (val < x) {
                curL.next = head;
                curL = curL.next;
            } else {
                curR.next = head;
                curR = curR.next;
            }
            head = head.next;
        }
        curL.next = dummyNodeR.next;
        // 特别注意：最后这一步不能忘记，否则会产生一个循环链表
        curR.next = null;
        return dummyNodeL.next;
    }
}

```
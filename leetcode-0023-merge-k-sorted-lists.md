# 23. Merge k Sorted Lists

## 题目描述和难度
+ 题目描述：合并 k 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。
+ 题目难度：困难。
+ 英文网址：[23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/description/)  。
+ 中文网址：[23. 合并K个排序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/description/)  。
## 思路分析
求解关键：这是一道类似于教科书上例题的问题。这里我们举生活中的例子来理解求解思路，其实一点都不难。
假设有如下生活情境：假设你是一名体育老师，有 3 个班的学生，他们已经按照身高从矮到高排好成了 3 列纵队，现在要把这 3 个班的学生也按照身高从矮到高排列一列纵队。我们可以这么做：
（1）让三个班的学生按列站在你的面前，这时你能看到站在队首的学生的全身，其余同学只能看到比前面同学脑袋高出的那部分；
（2）每一次队首的 3 名同学，请出最矮的同学出列到“队伍4”（即我们最终认为排好序的队列），出列的这一列的后一名同学向前走一步；
（3）重复第（2）步，直到 3 个班的同学全部出列完毕。

具体实现的时候，“每一次队首的 3 名同学，请出最矮的同学”这件事情可以交给优先队列去完成。在连续的两次出队之间完成“穿针引线”的工作，是不是很酷！下面的图说明了这样的过程。

<img src="https://liweiwei1419.github.io/images/leetcode-solution/23-1.jpg" width="600">

<img src="https://liweiwei1419.github.io/images/leetcode-solution/23-2.jpg" width="600">

<img src="https://liweiwei1419.github.io/images/leetcode-solution/23-3.jpg" width="600">

以上是思路1，对应参考解答1。下面介绍思路2，对应参考解答2：
根据之前处理链表的经验，如果我们不想“穿针引线”，那么递归方法是一个不错的选择，既然是数组的“排序”问题，我们不妨借助归并排序的**分治思想**来解决，代码结构和归并排序可以说是同出一辙。
1、先一分为二地解决了这个问题；
2、再考虑如何合并，这个合并的过程也是一个递归方法。

两种方法都利用到了常见的算法和基础的数据结构，值得学习和思考。

## 参考解答
### 参考解答1

```java
import java.util.Comparator;
import java.util.PriorityQueue;

class ListNode {
    int val;
    ListNode next;

    ListNode(int x) {
        val = x;
    }

    ListNode(Integer[] nums) {
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
        // 最后添加一个 NULL 标志表示添加到末尾了
        s.append("NULL");
        return s.toString();
    }
}

public class Solution {

    public ListNode mergeKLists(ListNode[] lists) {
        int len = lists.length;
        if (len == 0) {
            return null;
        }
        Comparator<ListNode> comparator = new Comparator<ListNode>() {
            @Override
            public int compare(ListNode o1, ListNode o2) {
                return o1.val - o2.val;
            }
        };
        PriorityQueue<ListNode> priorityQueue = new PriorityQueue<>(comparator);
        for (int i = 0; i < len; i++) {
            // 注意：这里要注意到测试用例中，ListNode 为 null 的特殊情况，空节点是一定不能放入优先队列的，把空节点放入优先队列没有意义
            if (lists[i] != null) {
                priorityQueue.add(lists[i]);
            }
        }
        ListNode dummyNode = new ListNode(-1);
        ListNode cur = dummyNode;
        while (!priorityQueue.isEmpty()) {
            ListNode curMin = priorityQueue.poll();
            cur.next = curMin;
            cur = cur.next;
            if (curMin.next != null) {
                priorityQueue.add(curMin.next);
            }
        }
        return dummyNode.next;
    }

    public static void main(String[] args) {
        Integer[] nums1 = {1, 4, 5};
        Integer[] nums2 = {1, 3, 4};
        Integer[] nums3 = {2, 6};
        ListNode head1 = new ListNode(nums1);
        ListNode head2 = new ListNode(nums2);
        ListNode head3 = new ListNode(nums3);
        ListNode[] lists = new ListNode[3];
        lists[0] = head1;
        lists[1] = head2;
        lists[2] = head3;
        Solution solution = new Solution();
        ListNode mergeKLists = solution.mergeKLists(lists);
        System.out.println(mergeKLists);
    }
}
```

### 参考解答2
```java
class Solution2 {
    public ListNode mergeKLists(ListNode[] lists) {
        int len = lists.length;
        if (len == 0) {
            return null;
        }
        return mergeKLists(lists, 0, len - 1);
    }

    private ListNode mergeKLists(ListNode[] lists, int l, int r) {
        if (l >= r) {
            return lists[l];
        }
        int mid = l + (r - l) / 2;
        ListNode listNode1 = mergeKLists(lists, l, mid);
        ListNode listNode2 = mergeKLists(lists, mid + 1, r);
        return mergeOfTwoListNode(listNode1, listNode2);
    }

    private ListNode mergeOfTwoListNode(ListNode listNode1, ListNode listNode2) {
        // 先处理递归到底的情况
        if (listNode1 == null) {
            return listNode2;
        }
        if (listNode2 == null) {
            return listNode1;
        }
        if (listNode1.val < listNode2.val) {
            // 把问题转化为一个更小的问题
            listNode1.next = mergeOfTwoListNode(listNode1.next, listNode2);
            return listNode1;
        } else {
            // 把问题转化为一个更小的问题
            listNode2.next = mergeOfTwoListNode(listNode1, listNode2.next);
            return listNode2;
        }
    }

}
```
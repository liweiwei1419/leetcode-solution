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
        PriorityQueue<ListNode> priorityQueue = new PriorityQueue<>(len, Comparator.comparingInt(a -> a.val));
        ListNode dummyNode = new ListNode(-1);
        ListNode curNode = dummyNode;
        for (ListNode list : lists) {
            if (list != null) {
                // 这一步很关键，不能也没有必要将空对象添加到优先队列中
                priorityQueue.add(list);
            }
        }
        while (!priorityQueue.isEmpty()) {
            // 优先队列非空才能出队
            ListNode node = priorityQueue.poll();
            // 当前节点的 next 指针指向出队元素
            curNode.next = node;
            // 当前指针向前移动一个元素，指向了刚刚出队的那个元素
            curNode = curNode.next;
            if (curNode.next != null) {
                // 只有非空节点才能加入到优先队列中
                priorityQueue.add(curNode.next);
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

说明：这里创建比较器对象还可以使用下面两种在 Java8 语言中使用的语法：

```java
Comparator<ListNode> comparator = (a, b) -> a.val - b.val;
```

与

```java
Comparator<ListNode> comparator = Comparator.comparingInt(a -> a.val);
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
        // // 思考这里为什么取等于？这是因为根据下文对 sort 的递归调用情况，区间最窄的时候，只可能是左右端点重合
        if (l >= r) {
            return lists[l];
        }
        int mid = l + (r - l) / 2;
        ListNode listNode1 = mergeKLists(lists, l, mid);
        ListNode listNode2 = mergeKLists(lists, mid + 1, r);
        // 于是问题转化成合并两个有序链表的问题了，我们可以穿针引线，也可以继续递归解决这个子问题，请见 LeetCode 第 21 题，
        // 这里我们使用继续递归解决，
        // 因为使用穿针引线，每一次调用这个方法的时候，都需要创建一个虚拟的头结点，归并次数有些多的时候，是不划算的
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
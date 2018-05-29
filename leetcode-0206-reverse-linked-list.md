# reverse-linked-list

## 题目描述和难度
+ 题目描述：反转一个单链表。
+ 题目难度：简单。
+ 英文网址：[206. reverse-linked-list]()  。
+ 中文网址：[206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/description/)  。
## 思路分析
求解关键：画图，这样思路和代码都会很清晰。  

<img src="https://liweiwei1419.github.io/images/leetcode-solution/206-1.jpg" width="500">

+ 在画图的过程中，我们就可以分析出完成翻转链表这件事情，一共要用 3 个指针 `pre`、`cur`、`next`：
1. 当前遍历的 `cur` 指针不必多说，是一定有的；
2. 当前结点的 next 指针要指到它前一个结点，所以 `pre` 也必须有；
3. 迭代要继续下去，`cur` 结点的下一个结点也得使用一个指针 `next` 保存一下，其中 `next` 可以在 `cur` 确定以后初始化；。

+ 画图分析 `next` 指针的指向，我们注意到我们分析出来的指针指向的先后顺序，通常跟数组的元素交换操作一样，程序写出来是“头尾相连”的，是不是很酷！  
+ 最后一定不要忘记，返回的是 `pre` 节点。

## 参考解答
### 参考解答1

```java
// https://leetcode-cn.com/problems/reverse-linked-list/description/
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

// 很常规的一道问题，关键在于画图分析
// 每一次遍历都要保证设立的 3 个指针的相对关系
// 注意，最后应该把 pre 指针返回

// 这个解法的时间复杂度是 O(n)，因为它仅仅遍历了一次链表，空间复杂度是 O(1)，因为这里仅仅使用了有限个的“指针”，帮助我们完成了链表的反转操作。
public class Solution {

    public ListNode reverseList(ListNode head) {
        // 初始化上一个指针
        ListNode pre = null;
        // 初始化当前指针
        ListNode cur = head;
        ListNode next;
        while (cur != null) {
            // 第 1 步：初始化 next 指针
            next = cur.next;
            // 第 2 步：实现当前节点的 next 指针的反转
            cur.next = pre;
            // 第 3 步：重新定义下一轮迭代的循环变量
            pre = cur;
            cur = next;
        }
        // 遍历完成以后，原来的最后一个节点就成为了 pre
        // 这个 pre 就是反转以后的新的链表的头指针
        return pre;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 4, 5};
        ListNode head = new  ListNode(nums);
        System.out.println(head);
        Solution solution = new Solution();
        ListNode reverseList = solution.reverseList(head);
        System.out.println("反转之后");
        System.out.println(reverseList);
    }
}
```



# map-sum-pairs

## 题目描述和难度
+ 题目描述：实现一个 MapSum 类里的两个方法，insert 和 sum。对于方法 insert，你将得到一对（字符串，整数）的键值对。字符串表示键，整数表示值。如果键已经存在，那么原来的键值对将被替代成新的键值对。对于方法 sum，你将得到一个表示前缀的字符串，你需要返回所有以该前缀开头的键的值的总和。
+ 题目难度：中等。
+ 英文网址：[677. Map Sum Pairs](https://leetcode.com/problems/map-sum-pairs/description/)  。
+ 中文网址：[677. 键值映射](https://leetcode-cn.com/problems/map-sum-pairs/description/)  。
## 思路分析
求解关键：使用 `Trie` 单词查找树这个数据结构来完成，将原来的 `isWord` 设计成 `value` 它不但可以表达原来 `isWord` 的含义，还能表示题目中一个单词携带的整数的含义。
+ 首先先把前缀遍历完，如果前缀都不能遍历完成，就说明单词查找树中不存在以这个单词为前缀的单词，应该返回 0，否则以一个结点为根，循环遍历到所有叶子节点，途径的所有 value 值都应该加和到最终的结果里。
+ 计算 sum 设计成一个递归方法，递归方法几行就完成了计算，虽然没有显式地写出递归终止条件，但递归终止条件已经包含在方法体中了。

## 参考解答
### 参考解答1

```java
import java.util.HashMap;

public class MapSum {

    private Node root;

    private class Node {
        private int value;
        private HashMap<Character, Node> next;

        public Node() {
            this(0);
        }

        public Node(int value) {
            this.value = value;
            this.next = new HashMap<>();
        }
    }

    /**
     * Initialize your data structure here.
     */
    public MapSum() {
        root = new Node();
    }

    public void insert(String key, int val) {
        Node curNode = root;
        for (int i = 0; i < key.length(); i++) {
            Character c = key.charAt(i);
            if (!curNode.next.containsKey(c)) {
                curNode.next.put(c, new Node());
            }
            curNode = curNode.next.get(c);
        }
        curNode.value = val;
    }

    // 设计一个递归函数去完成它
    public int sum(String prefix) {
        Node curNode = root;
        for (int i = 0; i < prefix.length(); i++) {
            Character c = prefix.charAt(i);
            if (curNode.next.containsKey(c)) {
                curNode = curNode.next.get(c);
            } else {
                return 0;
            }
        }
        return sum(curNode);
    }

    // 计算以 node 为根节点的所有 value 值的和
    private int sum(Node node) {
        int res = node.value;
        for (Character key : node.next.keySet()) {
            // 一直找到根节点
            res += sum(node.next.get(key));
        }
        return res;
    }

    public static void main(String[] args) {
        // 输入: insert("apple", 3), 输出: Null
        // 输入: sum("ap"), 输出: 3
        // 输入: insert("app", 2), 输出: Null
        // 输入: sum("ap"), 输出: 5
        MapSum2 mapSum = new MapSum2();
        mapSum.insert("apple", 3);
        int sum1 = mapSum.sum("ap");
        System.out.println(sum1);
        mapSum.insert("app", 2);
        int sum2 = mapSum.sum("ap");
        System.out.println(sum2);
    }
}
```
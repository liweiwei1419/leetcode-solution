# 208. Implement Trie (Prefix Tree)

## 题目描述和难度
+ 题目描述：实现一个 Trie (前缀树)，包含 `insert`, `search`, 和 `startsWith` 这三个操作。
+ 题目难度：中等。
+ 英文网址：[208. Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/description/)  。
+ 中文网址：[208. 实现 Trie (前缀树)](https://leetcode-cn.com/problems/implement-trie-prefix-tree/description/)  。
## 思路分析
求解关键：前缀树是一种高级的数据结构，不过实现起来并不困难。

<img src="https://liweiwei1419.github.io/images/leetcode-solution/" width="600">

## 参考解答
### 参考解答1

+ 注意：内部类 `Node` 的访问控制符要声明为 `private` ，否则不能得到 Accept 。

```java
import java.util.HashMap;

public class Trie {

    private Node root;

    // 只在内部使用，因此访问控制符是 root
    private class Node {
        private boolean isWord;
        // 不要忘记写上构造方法初始化 next 所对应的 Hash 表
        private HashMap<Character, Node> next;

        public Node() {
            this.isWord = false;
            this.next = new HashMap<>();
        }
    }

    /**
     * Initialize your data structure here.
     */
    public Trie() {
        // 根节点不表示任何字符
        root = new Node();
    }

    /**
     * Inserts a word into the trie.
     */
    public void insert(String word) {
        Node curNode = root;
        for (int i = 0; i < word.length(); i++) {
            Character c = word.charAt(i);
            if (!curNode.next.containsKey(c)) {
                curNode.next.put(c, new Node());
            }
            curNode = curNode.next.get(c);
        }
        // 如果之前没有设置过，才设置成 true
        if (!curNode.isWord) {
            curNode.isWord = true;
        }
    }

    /**
     * Returns if the word is in the trie.
     */
    public boolean search(String word) {
        Node curNode = root;
        for (int i = 0; i < word.length(); i++) {
            Character c = word.charAt(i);
            if (curNode.next.containsKey(c)) {
                curNode = curNode.next.get(c);
            } else {
                return false; // 中途就出错了
            }
        }
        return curNode.isWord; // 到了末尾还要判断一下
    }

    /**
     * Returns if there is any word in the trie that starts with the given prefix.
     */
    public boolean startsWith(String prefix) {
        Node curNode = root;
        for (int i = 0; i < prefix.length(); i++) {
            Character c = prefix.charAt(i);
            if (curNode.next.containsKey(c)) {
                curNode = curNode.next.get(c);
            } else {
                return false;
            }
        }
        // 能走完就说明有这个前缀
        return true;
    }

    public static void main(String[] args) {
        Trie trie = new Trie();
        trie.insert("apple");
        boolean search1 = trie.search("apple");// 返回 true
        System.out.println(search1);
        boolean search2 = trie.search("app");     // 返回 false
        System.out.println(search2);
        boolean startsWith = trie.startsWith("app");// 返回 true
        System.out.println(startsWith);
        trie.insert("app");
        boolean search3 = trie.search("app");     // 返回 true
        System.out.println(search3);
    }
}
```
# 77. Combinations

## 题目描述和难度
+ 题目描述：给定两个整数 n 和 k，返回 1 ... n 中所有可能的 k 个数的组合。
+ 题目难度：中等。
+ 英文网址：[77. Combinations](https://leetcode.com/problems/combinations/description/)  。
+ 中文网址：[77. 组合](https://leetcode-cn.com/problems/combinations/description/)  。
## 思路分析
求解关键：按顺序查找，已经用过的数字就不会再使用，因此不用设置 marked 数组。重点分析出遍历的 i 的上界是 `n - (k - stack.size()) + 1`。

<img src="https://liweiwei1419.github.io/images/leetcode-solution/77-1.jpg" width="600">

下面的图展示了如何分析出循环变量中 `i` 的上界。 （如果下面的图片太小，可以在图片上右键，选择“在新标签页中打开图片”，以查看大图。）

<img src="https://liweiwei1419.github.io/images/leetcode-solution/77-2.jpg" width="600">

## 参考解答
### 参考解答1

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Stack;

// https://leetcode-cn.com/problems/combinations/description/
public class Solution {

    private List<List<Integer>> res = new ArrayList<>();

    private void findCombinations(int n, int k, int begin, Stack<Integer> stack) {
        if (stack.size() == k) {
            // 够数了，就添加到结果集中
            res.add(new ArrayList<>(stack));
            return;
        }
        // n - (k - stack.size()) + 1 是一步剪枝操作
        // for (int i = index; i <= n; i++) {
        // 关键在于分析出 i 的上界
        for (int i = begin; i <= n - (k - stack.size()) + 1; i++) {
            stack.add(i);
            findCombinations(n, k, i + 1, stack);
            stack.pop();
        }
    }

    public List<List<Integer>> combine(int n, int k) {
        if (n <= 0 || k <= 0 || n < k) {
            return res;
        }
        // 从 1 开始是题目的设定
        findCombinations(n, k, 1, new Stack<>());
        return res;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        List<List<Integer>> combine = solution.combine(4, 2);
        System.out.println(combine);
    }
}
```
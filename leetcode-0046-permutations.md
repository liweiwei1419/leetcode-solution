# 46. Permutations

## 题目描述和难度
+ 题目描述：
给定一个没有重复数字的序列，返回其所有可能的全排列。
+ 题目难度：中等。
+ 英文网址：[46. Permutations](https://leetcode.com/problems/permutations/description/)  。
+ 中文网址：[46. 全排列](https://leetcode-cn.com/problems/permutations/description/)  。
## 思路分析
求解关键：画图理解题意并且打印出一些信息观察程序的执行流程。

<img src="https://liweiwei1419.github.io/images/leetcode-solution/46-1.jpg" width="600">

## 参考解答
### 参考解答1

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Stack;

// https://leetcode-cn.com/problems/permutations/description/
public class Solution {

    private List<List<Integer>> res = new ArrayList<>();
    // 设置是否使用的数组，也是套路了
    private int[] nums;
    private boolean[] marked;

    // hasUsedCount 表示已经使用的数组元素的个数
    private void findPermutions(int hasUsedCount, Stack<Integer> stack) {
        // 这一行代码是调试信息，可以帮助我们观察程序的执行流程
        // System.out.println(Arrays.toString(used));
        if (hasUsedCount == nums.length) {
            // 添加到结果集中
            res.add(new ArrayList<>(stack));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (!marked[i]) {
                marked[i] = true;
                stack.push(nums[i]);
                findPermutions(hasUsedCount + 1, stack);
                stack.pop();
                marked[i] = false;
            }
        }
    }

    public List<List<Integer>> permute(int[] nums) {
        int len = nums.length;
        if (len == 0) {
            return res;
        }
        this.nums = nums;
        marked = new boolean[len];
        findPermutions(0, new Stack<>());
        return res;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3};
        Solution solution = new Solution();
        List<List<Integer>> permute = solution.permute(nums);
        System.out.println(permute);
    }
}
```
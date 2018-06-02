# 47. Permutations II

## 题目描述和难度
+ 题目描述：给定一个可包含重复数字的序列，返回所有不重复的全排列。
+ 题目难度：中等。
+ 英文网址：[47. Permutations II](https://leetcode.com/problems/permutations-ii/description/)  。
+ 中文网址：[47. 全排列 II](https://leetcode-cn.com/problems/permutations-ii/description/)  。
## 思路分析
求解关键：找到重复的原因，对树进行剪枝。
1、**首先将数组排序**，这一步很关键，是后面剪枝的基础；
2、只处理第 1 次遇到的那个数，举个具体的例子画个图。重点理解：（1） `i > 0` ，（2） `nums[i] == nums[i - 1]` ，（3）之前那个数还没有使用，即 `marked[i-1] = false`。

<img src="https://liweiwei1419.github.io/images/leetcode-solution/47-1.jpg" width="600">

## 参考解答
### 参考解答1

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Stack;

public class Solution {

    private List<List<Integer>> res = new ArrayList<>();
    private boolean[] marked;

    private void findPermuteUnique(int[] nums, int depth, Stack<Integer> stack) {
        if (depth == nums.length) {
            res.add(new ArrayList<>(stack));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (!marked[i]) {
                // i > 0 是为了保证 marked[i - 1] 有意义，事实上 i = 0 是一定在解当中的
                // 相当于树被剪枝，重点体会这一步剪枝操作是为什么，其实画个图就非常清楚了
                if (i > 0 && nums[i] == nums[i - 1] && !marked[i - 1]) {
                    continue;
                }
                marked[i] = true;
                stack.add(nums[i]);
                findPermuteUnique(nums, depth + 1, stack);
                stack.pop();
                marked[i] = false;
            }
        }
    }

    public List<List<Integer>> permuteUnique(int[] nums) {
        int len = nums.length;
        if (len == 0) {
            return res;
        }
        // 这一步很关键，是后面剪枝的基础
        Arrays.sort(nums);
        marked = new boolean[len];
        findPermuteUnique(nums, 0, new Stack<>());
        return res;
    }

    public static void main(String[] args) {
        int[] nums = {1, 1, 2};
        Solution solution = new Solution();
        List<List<Integer>> permuteUnique = solution.permuteUnique(nums);
        System.out.println(permuteUnique);
    }
}
```
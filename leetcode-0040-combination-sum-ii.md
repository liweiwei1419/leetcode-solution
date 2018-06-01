# 40. Combination Sum II

## 题目描述和难度
+ 题目描述：给定一个数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。candidates 中的每个数字在每个组合中只能使用一次。
+ 题目难度：中等。
+ 英文网址：[40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/description/)  。
+ 中文网址：[40. 组合总和 II](https://leetcode-cn.com/problems/combination-sum-ii/description/)  。
## 思路分析
求解关键：找到如何在结果集中去除重复的方法。
（1）与第 39 题的区别，第 39 题的数组没有重复数字，可以使用多次；第 40 题的数组有重复数字，只能使用一次，具体就体现在进行下一层递归的时候，起始的那个索引值是多少；  
（2）很容易想到，应该先对给出的数组进行排序，排序的目的有两个：其一是，可以提前终止循环，其二是“在递归函数的调用中，同一深度的一个值只能使用一次”，这一处理也几乎成为了标准写法，或许刚刚开始接触的时候并不好理解，应该使用具体的例子画出图来理解，然后多做一些类似练习，理解代码为什么那样写。

## 参考解答
### 参考解答1

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Stack;

public class Solution {

    private List<List<Integer>> res = new ArrayList<>();
    private int[] candidates;
    private int len;

    // residue 表示剩余，这个值一开始等于 target，基于题目中说明的"所有数字（包括目标数）都是正整数"这个条件
    // residue 在递归遍历中，只会越来越小
    private void findCombinationSum2(int residue, int begin, Stack<Integer> stack) {
        if (residue == 0) {
            res.add(new ArrayList<>(stack));
            return;
        }
        for (int i = begin; i < len && residue - candidates[i] >= 0; i++) {
            // 这一步之所以能够生效，其前提是数组一定是排好序的，这样才能保证：
            // 在递归调用的统一深度（层）中，一个元素只使用一次。
            // 这一步剪枝操作基于 candidates 数组是排序数组的前提下
            if (i > begin && candidates[i] == candidates[i - 1]) {
                continue;
            }
            stack.add(candidates[i]);
            // 【关键】因为元素不可以重复使用，这里递归传递下去的是 i + 1 而不是 i
            findCombinationSum2(residue - candidates[i], i + 1, stack);
            stack.pop();
        }
    }

    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        int len = candidates.length;
        if (len == 0) {
            return res;
        }
        this.len = len;
        // 先将数组排序，这一步很关键
        Arrays.sort(candidates);
        this.candidates = candidates;
        findCombinationSum2(target, 0, new Stack<>());
        return res;
    }

    public static void main(String[] args) {
        int[] candidates = {2, 5, 2, 1, 2};
        int target = 5;
        Solution solution = new Solution();
        List<List<Integer>> combinationSum2 = solution.combinationSum2(candidates, target);
        System.out.println(combinationSum2);
    }
}
```
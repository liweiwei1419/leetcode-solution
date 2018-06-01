# 39. Combination Sum

## 题目描述和难度
+ 题目描述：给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。candidates 中的数字可以无限制重复被选取。说明：所有数字（包括 target）都是正整数。解集不能包含重复的组合。 
+ 题目难度：中等。
+ 英文网址：[39. Combination Sum](https://leetcode.com/problems/combination-sum/description/)  。
+ 中文网址：[39. 组合总和](https://leetcode-cn.com/problems/combination-sum/description/)  。
## 思路分析
求解关键：注意分析题意，找到可以减少判断的条件：
（1）这道题猛地一看好像跟前面的问题搭不上关系，因为题目中说“candidates 中的数字可以无限制重复被选取”；  
（2）但其实仔细想想就会发现，我们每次取数字的时候，还从原点开始取就行了呀，是不是很酷；  
（3）为了达到提前判断循环结束的效果，我们可以先对数组排个序，如果起点数字比剩下的和还要大，后面的循环就没有必要进行下去了。此时，我们在 for 循环里加判断，尽量减少了系统栈的调用深度。

## 参考解答
### 参考解答1（没有做优化剪枝的版本）

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Stack;

public class Solution {

    private List<List<Integer>> res = new ArrayList<>();
    private int[] candidates;
    private int len;

    // residue 定义为剩余，这个剩余一开始等于 target，在递归中，它的值会越来越小
    // 因为题目中说了"所有数字（包括 target）都是正整数"。
    private void findCombinationSum(int residue, int start, Stack<Integer> pre) {
        // 因为可以无限选取，所以 residue 只能小于 0 或者等于 0
        if (residue < 0) {
            return;
        }
        // 一定是剩下的那个数为 0 了，才表示我们所选的数字的和刚好等于 target
        if (residue == 0) {
            res.add(new ArrayList<>(pre));
            return;
        }
        for (int i = start; i < len; i++) {
            // 每个数有选择和不选择，因此尝试了一种解的可能以后要进行状态重置
            pre.add(candidates[i]);
            // 【关键】因为元素可以重复使用，这里递归传递下去的是 i 而不是 i + 1
            findCombinationSum(residue - candidates[i], i, pre);
            pre.pop();
        }
    }

    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        int len = candidates.length;
        if (len == 0) {
            return res;
        }
        this.len = len;
        this.candidates = candidates;
        findCombinationSum(target, 0, new Stack<>());
        return res;
    }

    public static void main(String[] args) {
        int[] candidates = {2, 3, 6, 7};
        int target = 7;
        Solution solution = new Solution();
        List<List<Integer>> combinationSum = solution.combinationSum(candidates, target);
        System.out.println(combinationSum);
    }
}
```

### 参考解答2（推荐）
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Stack;

public class Solution2 {

    private List<List<Integer>> res = new ArrayList<>();
    private int[] candidates;
    private int len;

    private void findCombinationSum(int residue, int start, Stack<Integer> pre) {
        if (residue == 0) {
            res.add(new ArrayList<>(pre));
            return;
        }
        // 优化添加的代码2：在循环的时候做判断，尽量避免系统栈的深度
        // residue - candidates[i] 表示下一轮的剩余，如果下一轮的剩余都小于 0 ，就没有必要进行后面的循环了
        // 这一点基于原始数组是排序数组的前提，因为如果计算后面的剩余，只会越来越小
        for (int i = start; i < len && residue - candidates[i] >= 0; i++) {
            pre.add(candidates[i]);
            // 【关键】因为元素可以重复使用，这里递归传递下去的是 i 而不是 i + 1
            findCombinationSum(residue - candidates[i], i, pre);
            pre.pop();
        }
    }

    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        int len = candidates.length;
        if (len == 0) {
            return res;
        }
        // 优化添加的代码1：先对数组排序，可以提前终止判断
        Arrays.sort(candidates);
        this.len = len;
        this.candidates = candidates;
        findCombinationSum(target, 0, new Stack<>());
        return res;
    }
}
```
# 377. Combination Sum IV

## 题目描述和难度
+ 题目描述：给定一个由正整数组成且不存在重复数字的数组，找出和为给定目标正整数的组合的个数。
+ 题目难度：中等。
+ 英文网址：[377. Combination Sum IV](https://leetcode.com/problems/combination-sum-iv/description/)  。
+ 中文网址：[377. Combination Sum IV](https://leetcode-cn.com/problems/combination-sum-iv/description/)  。
## 思路分析
求解关键：按照下图所示的规律找到**递归关系式**，体会我们在这道题的求解过程中是如何进行搜索的，我们不是胡乱搜索，而是按照顺序搜索：每次都减去一枚硬币的值，看减去了一枚硬币的剩余价值的组合个数有多少，和没有减去这枚硬币的价值的组合个数建立关系。

<img src="https://liweiwei1419.github.io/images/leetcode-solution/377-1.jpg" width="600">

## 参考解答
### 参考解答1

```java
public class Solution {

    public int combinationSum4(int[] nums, int target) {
        int[] dp = new int[target + 1];
        // 这一步很关键，想想为什么 dp[0] 是 1
        // 因为 0 表示空集，空集和它"前面"的元素凑成一种解法，所以是 1
        // 这一步要加深体会
        dp[0] = 1;
        for (int i = 1; i < target + 1; i++) {
            for (int num : nums) {
                if (i >= num) {
                    dp[i] = dp[i] + dp[i - num];
                }
            }
        }
        return dp[target];
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] nums = {1, 2, 3};
        int target = 4;
        int combinationSum4 = solution.combinationSum4(nums, target);
        System.out.println(combinationSum4);
    }
}

```
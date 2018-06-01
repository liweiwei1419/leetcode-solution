# 17. Letter Combinations of a Phone Number

## 题目描述和难度
+ 题目描述：电话号码的字母组合。给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。
+ 题目难度：中等。
+ 英文网址：[17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)  。
+ 中文网址：[17. 电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/description/)  。
## 思路分析
求解关键：使用回溯的方式进行搜索求解。

对于问题的考虑：
1、字符串的合法性（能出现什么样的字符串，“@”可以吗？“1”可以吗？）：不可以，只能出现 2、3、4、5、6、7、8、9。
2、空字符串（如果给出的是空字符串，返回什么）：返回空列表，即元素个数为 0 的列表。
3、多个解的顺序？题目已经告诉了我们，这个问题中对顺序没有要求。
我认为，这个问题更像数学问题中的乘法计数原理：第 1 步，考虑数字 2 能表达的三个字母；第 2 步，考虑 3 能表达的三个字母。于是，我们最容易想到用多重循环来解决这个问题。但是在步数很多的时候，循环就变得低效了。此时，递归回溯这个技巧就可以派上用场了。

思考总结：
1、为什么我们要再写一个函数，而不是直接在原来的 letterCombinations 函数中书写呢？递归过程是把一个规模较大的问题一步一步地转化成为一个规模更小的问题，而我们发现的递归关系并不能用 letterCombinations 函数来描述，也就是说这个规模更小的问题，不能使用 letterCombinations() 来表述；
2、细节考虑要周到：我们在使用递归方法解决问题的时候，一定不能忽略边界的情况的处理；同时递归终止条件要仔细考虑，特别是对边界的情况；
3、如何设计递归方法其实是有固定模式的，参数的设定也是有规律的，无非是弄清楚之前是什么，当前是什么，然后把当前的加到之前的；
4、对于数字字符转换为数字，这里使用的是 `digits.charAt(index) - '0'`；
5、严格意义上说，还要对所输入的数字字符的合法性作判断，例如：`assert c >= '0' || c <= '9' || c != '1';`；
6、findCombination 函数中的 digitsMap 可以写成成员变量；
7、这里因为 String 是不可变对象，所以每一次的方法调用，其实都是新的对象传递下去，这一点在我们后续的练习中要留意（这句话表达比较隐晦，要深刻理解这个事实还要做后面的练习，当 result 是其它类型的对象的时候，就不能简单的 add 操作了）。
8、可以看到，递归回溯的结果是很整齐的，在后序的学习中我们就会看到，递归回溯是深度优先遍历的一种体现。

## 参考解答
### 参考解答1

```java
import java.util.ArrayList;
import java.util.List;

public class Solution {

    private List<String> res = new ArrayList<>();
    private String[] digitsMap = {
            " ", "", "abc", "def", "ghi", "jkl", "mno",
            "pqrs", "tuv", "wxyz"
    };

    private void findCombinations(String digits, int begin, String pre) {
        // 先写递归终止条件
        if (begin == digits.length()) {
            res.add(pre);
            return;
        }
        String nextStr = digitsMap[digits.charAt(begin) - '0'];
        // 理解这段代码的时候，一定要结合题意，因为那个数字所对应的字符串中的每个字符都要考虑到，所以要使用循环
        for (int i = 0; i < nextStr.length(); i++) {
            findCombinations(digits, begin + 1, pre + nextStr.charAt(i));
        }
    }

    public List<String> letterCombinations(String digits) {
        if (digits.length() == 0) {
            return res;
        }
        findCombinations(digits, 0, "");
        return res;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        List<String> letterCombinations = solution.letterCombinations("23");
        System.out.println(letterCombinations);
    }
}
```
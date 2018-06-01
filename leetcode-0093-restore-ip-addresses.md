# 93. Restore IP Addresses

## 题目描述和难度
+ 题目描述：
+ 题目难度：中等。
+ 英文网址：[93. Restore IP Addresses](https://leetcode.com/problems/restore-ip-addresses/description/)  。
+ 中文网址：[93. 复原IP地址](https://leetcode-cn.com/problems/restore-ip-addresses/description/)  。
## 思路分析
求解关键：使用深度优先遍历、递归回溯的思想来完成。

1、IP 地址一共 4 段，每一段的最大值是 255，最小值是 0，我们采用搜索的办法来得到有效的 ip 段；
2、每一次循环判断接下来读进来的 3 个数字字符是有可能成为一个 ip 段，如果可以，加到已经形成的 ip 段后面（特别要注意，截取字符串的时候不能越界）；
3、接下来递归终止的条件就得分析清楚了，但是也不是难事，把握好总共分 4 段，当画上第 4 个点，并且下一个考察的下标已经“刚刚好”越界的时候，此时，我们就找到了一个有效的 ip 段分割。


## 参考解答
### 参考解答1

```java
import java.util.ArrayList;
import java.util.List;

// https://leetcode-cn.com/problems/restore-ip-addresses/description/
public class Solution {

    private List<String> res = new ArrayList<>();

    private boolean judgeIfIPSegment(String ipSegment) {
        int len = ipSegment.length();
        // 大于 1 位的时候，不能以 0 开头
        if (len > 1 && ipSegment.startsWith("0")) {
            return false;
        }
        return Integer.parseInt(ipSegment) <= 255;
    }

    private void findIpSegment(String s, int split, int begin, String pre) {
        // 先写递归终止条件
        if (split == 4) {
            if (begin == s.length()) {
                res.add(pre.substring(0, pre.length() - 1));
            }
            return;
        }
        // split < 4 的时候
        // begin + i <= s.length() 容易被忽略
        for (int i = 1; i <= 3 && begin + i <= s.length(); i++) {
            // 可能成为 ip 段的字符串
            String ifIpSegment = s.substring(begin, begin + i);
            if (judgeIfIPSegment(ifIpSegment)) {
                findIpSegment(s, split + 1, begin + i, pre + ifIpSegment + '.');
            }
        }

    }

    public List<String> restoreIpAddresses(String s) {
        int len = s.length();
        if (len == 0) {
            return res;
        }
        findIpSegment(s, 0, 0, "");
        return res;
    }

    public static void main(String[] args) {
        String s = "25525511135";
        Solution solution = new Solution();
        List<String> restoreIpAddresses = solution.restoreIpAddresses(s);
        System.out.println(restoreIpAddresses);
    }
}
```
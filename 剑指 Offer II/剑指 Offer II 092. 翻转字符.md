### [剑指 Offer II 092. 翻转字符](https://leetcode.cn/problems/cyJERH/)

### 动态规划

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int minFlipsMonoIncr(string s) {
        int ones = 0, cnt = 0;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '1') ones++;       // 1 的个数
            else cnt = min(cnt + 1, ones);  // 0->1，翻转前面的 1
        }
        return cnt;
    }
};
```

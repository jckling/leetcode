### [剑指 Offer II 097. 子序列的数目](https://leetcode.cn/problems/21dk04/)

### 动态规划

`dp[i][j]` 表示 s 中的前 i 个字符中，出现 t 中的前 j 个字符的次数

- 时间复杂度：O(mn)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int numDistinct(string s, string t) {
        int m = s.size(), n = t.size();
        
        // 当前行
        vector<uint64_t> dp(n + 1, 0);
        dp[0] = 1;

        // 上一行
        vector<uint64_t> pre(n + 1, 0);
        pre[0] = 1;

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (s[i - 1] == t[j - 1]) dp[j] += pre[j - 1];
                pre[j - 1] = dp[j - 1];
            }
        }

        return dp[n];
    }
};
```

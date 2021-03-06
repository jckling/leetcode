### [剑指 Offer 19. 正则表达式匹配](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/)

### 动态规划

- 时间复杂度：O(mn)
- 空间复杂度：O(mn)

```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.size(), n = p.size();

        // dp[i][j] 表示 s[:i] 与 p[:j] 是否可以匹配
        vector<vector<bool>> dp(m + 1, vector<bool>(n + 1, false));
        dp[0][0] = true;    // 两个空字符串可以匹配

        // 初始化首行
        for (int j = 2; j <= n; j += 2) {
            // p 偶数位为 * 时才能匹配
            dp[0][j] = dp[0][j - 2] && p[j - 1] == '*';
        }

        // 状态转移
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (p[j - 1] == '*') {
                    if (dp[i][j - 2]) dp[i][j] = true;                              // p[j - 2] * 出现 0 次
                    else if (dp[i - 1][j] && s[i - 1] == p[j - 2]) dp[i][j] = true; // p[j - 2] 多出现 1 次
                    else if (dp[i - 1][j] && p[j - 2] == '.') dp[i][j] = true;      // . 多出现 1 次
                }
                else {
                    if (dp[i - 1][j - 1] && s[i - 1] == p[j - 1]) dp[i][j] = true;  // p[j - 1] 多出现 1 次
                    else if (dp[i - 1][j - 1] && p[j - 1] == '.') dp[i][j] = true;  // 将 . 看作 s[i - 1]
                }
            }
        }

        return dp[m][n];
    }
};
```

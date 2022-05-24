### [剑指 Offer II 095. 最长公共子序列](https://leetcode.cn/problems/qJnOS7/)

### 动态规划

`dp[i][j]` 表示字符串 text1 的 `[1,i]` 区间和字符串 text2 的 `[1,j]` 区间的最长公共子序列长度。

- 时间复杂度：O(mn)
- 空间复杂度：O(mn)

```c++
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int m = text1.size(), n = text2.size();
        vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1[i - 1] == text2[j - 1]) dp[i][j] = dp[i - 1][j - 1] + 1;
                else dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
        return dp[m][n];
    }
};
```

### [剑指 Offer II 096. 字符串交织](https://leetcode.cn/problems/IY6buf/)

### 动态规划

`dp[i][j]` 表示 s1 的前 i 个字符和 s2 的前 j 个字符是否能组成 s3 的前 i+j 个字符。

- 时间复杂度：O(mn)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    bool isInterleave(string s1, string s2, string s3) {
        int m = s1.size(), n = s2.size(), t = s3.size();
        if (m + n != t) return false;

        vector<int> f(n + 1, false);
        f[0] = true;
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                int p = i + j - 1;
                // s1[i - 1] == s3[i + j - 1]
                if (i > 0) f[j] &= (s1[i - 1] == s3[p]);
                // s2[j - 1] == s3[i + j - 1]
                if (j > 0) f[j] |= (f[j - 1] && s2[j - 1] == s3[p]);
            }
        }

        return f[n];
    }
};
```

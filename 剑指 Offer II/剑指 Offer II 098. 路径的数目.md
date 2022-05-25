### [剑指 Offer II 098. 路径的数目](https://leetcode.cn/problems/2AoeFn/)

### 动态规划

- 时间复杂度：O(mn)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<int> dp(n);
        for (int j = 0; j < n; j++) dp[j] = 1;

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[j] += dp[j - 1];
            }
        }
        return dp[n - 1];
    }
};
```

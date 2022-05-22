### [剑指 Offer 47. 礼物的最大价值](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/)

### 动态规划

- 时间复杂度：O(mn)
- 空间复杂度：O(mn)

```c++
class Solution {
public:
    int maxValue(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();
        vector<vector<int>> dp(m + 1, vector<int>(n + 1));

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                dp[i][j] = grid[i - 1][j - 1] + max(dp[i - 1][j], dp[i][j - 1]);
            }
        }

        return dp[m][n];
    }
};
```

优化空间复杂度 O(1)

```c++
class Solution {
public:
    int maxValue(vector<vector<int>>& grid) {
        int n = grid.size(), m = grid[0].size();
        for(int j = 1; j < m; j++) grid[0][j] += grid[0][j - 1];    // 第一行
        for(int i = 1; i < n; i++) grid[i][0] += grid[i - 1][0];    // 第一列

        for(int i = 1; i < n; i++) {
            for(int j = 1; j < m; j++) {
                grid[i][j] += max(grid[i][j - 1], grid[i - 1][j]);
            }
        }

        return grid[n - 1][m - 1];
    }
};
```

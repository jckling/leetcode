### [剑指 Offer II 107. 矩阵中的距离](https://leetcode.cn/problems/2bCMpM/)

### BFS

- 时间复杂度：O(mn)
- 空间复杂度：O(mn)

```c++
class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        int m = mat.size(), n = mat[0].size();
        queue<pair<int, int>> q;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (mat[i][j] == 0) q.push({i, j});
                else mat[i][j] = m + n; // 最大值
            }
        }
        
        int dx[4] = {0, 1, 0, -1};
        int dy[4] = {1, 0, -1, 0};
        while (!q.empty()) {
            auto [x, y] = q.front();
            q.pop();
            for (int i = 0; i < 4; i++) {
                int r = x + dx[i], c = y + dy[i];
                if (r < 0 || r >= m || c < 0 || c >= n || mat[r][c] <= mat[x][y]) continue;
                mat[r][c] = mat[x][y] + 1;
                q.push({r, c});
            }
        }

        return mat;
    }
};
```

### 动态规划

- 时间复杂度：O(mn)
- 空间复杂度：O(mn)

```c++
class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        int m = mat.size(), n = mat[0].size();
        vector<vector<int>> dp(m, vector<int>(n, m + n));
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (mat[i][j] == 0) dp[i][j] = 0;
            }
        }
        
        // i       j       方向        已搜索完毕
        // 0->n    0->m    左上->右下  i-1, j-1
        // n->0    m->0    右下->左上  i+1, j+1

        // f(i, j) = 0, mat[i][j] == 0
        // f(i, j) = 1 + min(f(i - 1, j), f(i, j - 1)), mat[i][j] == 1

        // 左上 -> 右下
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (i - 1 >= 0) dp[i][j] = min(dp[i][j], dp[i - 1][j] + 1);
                if (j - 1 >= 0) dp[i][j] = min(dp[i][j], dp[i][j - 1] + 1);
            }
        }

        // 右下 -> 左上
        for (int i = m - 1; i >= 0; i--) {
            for (int j = n - 1; j >= 0; j--) {
                if (i + 1 < m) dp[i][j] = min(dp[i][j], dp[i + 1][j] + 1);
                if (j + 1 < n) dp[i][j] = min(dp[i][j], dp[i][j + 1] + 1);
            }
        }

        return dp;
    }
};
```

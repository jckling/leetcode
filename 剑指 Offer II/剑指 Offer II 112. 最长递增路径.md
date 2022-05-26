### [剑指 Offer II 112. 最长递增路径](https://leetcode.cn/problems/fpTFWP/)

### DFS

记忆化搜索

- 时间复杂度：O(mn)
- 空间复杂度：O(mn)

```c++
class Solution {
public:
    int longestIncreasingPath(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        vector<vector<int>> memo(m, vector<int>(n, 0));

        int ans = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                ans = max(ans, dfs(matrix, i, j, memo));
            }
        }
        return ans;
    }
private:
    int dx[4] = {1, 0, -1, 0};
    int dy[4] = {0, 1, 0, -1};
    int dfs(vector<vector<int>>& matrix, int x, int y, vector<vector<int>>& memo) {
        if (memo[x][y] != 0) return memo[x][y];
        
        memo[x][y]++;
        for (int i = 0; i < 4; i++) {
            int r = x + dx[i], c = y + dy[i];
            if (r < 0 || r >= matrix.size() || c < 0 || c >= matrix[0].size() || matrix[r][c] <= matrix[x][y]) continue;
            memo[x][y] = max(memo[x][y], dfs(matrix, r, c, memo) + 1);
        }
        return memo[x][y];
    }
};
```

### 拓扑排序

- 时间复杂度：O(mn)
- 空间复杂度：O(mn)

```c++
class Solution {
public:
    int longestIncreasingPath(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        vector<vector<int>> odg(m, vector<int>(n, 0));
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                for (int k = 0; k < 4; k++) {
                    int x = i + dx[k], y = j + dy[k];
                    if (x < 0 || x >= m || y < 0 || y >= n || matrix[x][y] <= matrix[i][j]) continue;
                    ++odg[i][j];    // 出度，小 -> 大
                }
            }
        }

        queue<pair<int, int>> q;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (odg[i][j] == 0) q.push({i, j});
            }
        }

        int ans = 0;
        while (!q.empty()) {
            ans++;
            int size = q.size();
            while (size--) {
                auto [i, j] = q.front();
                q.pop();
                for (int k = 0; k < 4; k++) {
                    int x = i + dx[k], y = j + dy[k];
                    if (x < 0 || x >= m || y < 0 || y >= n || matrix[x][y] >= matrix[i][j]) continue;
                    if (--odg[x][y] == 0) q.push({x, y});   // 指向当前节点的出度减小
                }
            }
        }

        return ans;
    }
private:
    int dx[4] = {1, 0, -1, 0};
    int dy[4] = {0, 1, 0, -1};
};
```

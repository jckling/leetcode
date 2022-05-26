### [剑指 Offer II 105. 岛屿的最大面积](https://leetcode.cn/problems/ZL6zAn/)

### DFS

- 时间复杂度：O(mn)
- 空间复杂度：O(mn)

```c++
class Solution {
public:
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        int ans = 0;
        for (int i = 0; i < grid.size(); i++) {
            for (int j = 0; j < grid[0].size(); j++) {
                if (grid[i][j] == 1) ans = max(ans, dfs(grid, i, j));
            }
        }
        return ans;
    }
private:
    int dfs(vector<vector<int>>& grid, int x, int y) {
        if (x < 0 || x >= grid.size() || y < 0 || y >= grid[0].size() || grid[x][y] == 0) return 0;

        grid[x][y] = 0;
    
        int cnt = 1;
        cnt += dfs(grid, x + 1, y);
        cnt += dfs(grid, x, y + 1);
        cnt += dfs(grid, x - 1, y);
        cnt += dfs(grid, x, y - 1);

        return cnt;
    }
};
```

### BFS

- 时间复杂度：O(mn)
- 空间复杂度：O(mn)

```c++
class Solution {
public:
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        int ans = 0;
        queue<pair<int, int>> q;
        for (int i = 0; i < grid.size(); i++) {
            for (int j = 0; j < grid[0].size(); j++) {
                if (grid[i][j] == 1) q.push({i, j});
                int cnt = 0;
                while (!q.empty()) {
                    auto [x, y] = q.front();
                    q.pop();

                    if (x < 0 || x >= grid.size() || y < 0 || y >= grid[0].size() || grid[x][y] == 0) continue;
                    
                    grid[x][y] = 0;
                    cnt++;

                    q.push({x + 1, y});
                    q.push({x, y + 1});
                    q.push({x - 1, y});
                    q.push({x, y - 1});
                }
                ans = max(ans, cnt);
            }
        }

        return ans;
    }
};
```

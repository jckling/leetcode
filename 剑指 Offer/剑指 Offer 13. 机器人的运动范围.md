### [剑指 Offer 13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

### DFS

- 时间复杂度：O(mn)
- 空间复杂度：O(mn)

```c++
class Solution {
public:
    int movingCount(int m, int n, int k) {
        vector<vector<bool>> visited(m, vector<bool>(n, 0));
        return dfs(0, 0, visited, m, n, k);
    }
private:
    int sum(int a) {
        int res = 0;
        while(a) {
            res += a % 10;
            a /= 10;
        }
        return res;
    }
    int dfs(int i, int j, vector<vector<bool>>& visited, int m, int n, int k) {
        if(i >= m || j >= n || sum(i) + sum(j) > k || visited[i][j]) return 0;

        visited[i][j] = true;
        // 剪枝：只考虑往右、往下
        return 1 + dfs(i + 1, j, visited, m, n, k) + dfs(i, j + 1, visited, m, n, k);
    }
};
```

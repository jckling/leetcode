### [剑指 Offer II 116. 省份数量](https://leetcode.cn/problems/bLyHh0/)

### DFS

- 时间复杂度：O(n^2)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n = isConnected.size();
        vector<bool> visited(n, false);
        int cnt = 0;
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                cnt++;
                dfs(isConnected, i, visited);
            }
        }
        return cnt;
    }
private:
    void dfs(vector<vector<int>>& isConnected, int idx, vector<bool>& visited) {
        visited[idx] = true;
        for (int i = 0; i < isConnected.size(); i++) {
            if (isConnected[idx][i] == 1 && !visited[i]) dfs(isConnected, i, visited);
        }
    }
};
```

### BFS

- 时间复杂度：O(n^2)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n = isConnected.size();
        vector<bool> visited(n, false);
        int cnt = 0;
        queue<int> q;
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                q.push(i);
                while (!q.empty()) {
                    int j = q.front();
                    q.pop();
                    visited[j] = true;
                    for (int k = 0; k < n; k++) {
                        if (isConnected[j][k] == 1 && !visited[k]) q.push(k);
                    }
                }
                cnt++;
            }
        }
        return cnt;
    }
};
```

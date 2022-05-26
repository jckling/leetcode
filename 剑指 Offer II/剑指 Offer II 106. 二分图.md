### [剑指 Offer II 106. 二分图](https://leetcode.cn/problems/vEAB3K/)

### DFS

- 时间复杂度：O(m+n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    bool isBipartite(vector<vector<int>>& graph) {
        int n = graph.size();
        vector<int> visited(n); // -1、1 表示染色
        for (int i = 0; i < n; i++) {
            if (visited[i] == 0 && !dfs(graph, i, 1, visited)) return false;
        }
        return true;
    }
private:
    bool dfs(vector<vector<int>>& graph, int idx, int color, vector<int>& visited) {
        if (visited[idx] != 0) return visited[idx] == color;

        visited[idx] = color;
        for (auto& neighbor : graph[idx]) {
            if (!dfs(graph, neighbor, -color, visited)) return false;
        }

        return true;
    }
};
```

### BFS

- 时间复杂度：O(m+n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    bool isBipartite(vector<vector<int>>& graph) {
        int n = graph.size();
        vector<int> visited(n); // -1、1 表示染色
        queue<int> q;
        for (int i = 0; i < n; i++) {
            if (visited[i] != 0) continue;
            q.push(i);
            visited[i] = 1;
            while (!q.empty()) {
                int node = q.front();
                q.pop();
                for (auto& neighbor : graph[node]) {
                    if (visited[neighbor] == visited[node]) return false;
                    if (visited[neighbor] == 0) {
                        q.push(neighbor);
                        visited[neighbor] = -visited[node];
                    }
                }
            }
        }
        return true;
    }
};
```

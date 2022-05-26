### [剑指 Offer II 110. 所有路径](https://leetcode.cn/problems/bP4bmD/)

### DFS

- 时间复杂度：$O(n*2^n)$
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
        path.push_back(0);
        dfs(graph, graph.size() - 1, 0);
        return ans;
    }
private:
    vector<vector<int>> ans;
    vector<int> path;
    void dfs(vector<vector<int>>& g, int n, int idx) {
        if (idx == n) {
            ans.push_back(path);
            return;
        }
        for (auto& neighbor : g[idx]) {
            path.push_back(neighbor);
            dfs(g, n, neighbor);
            path.pop_back();
        }
    }
};
```

### [剑指 Offer II 118. 多余的边](https://leetcode.cn/problems/7LpjUW/)

### 并查集

求多余的连通分量。

- 时间复杂度：O(nlogn)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        init(edges.size());
        for (auto& e : edges) {
            int x = e[0], y = e[1];
            if (find(x) != find(y)) _union(x, y);
            else return e;
        }
        return {};
    }
private:
    vector<int> p;
    void init(int n) {
        p.resize(n + 1);
        for (int i = 1; i <= n; i++) p[i] = i;
    }

    int find(int x) {
        if (p[x] != x) p[x] = find(p[x]);
        return p[x];
    }

    void _union(int x, int y) {
        int px = find(x), py = find(y);
        p[px] = py;
    }
};
```

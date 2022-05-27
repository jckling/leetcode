### [剑指 Offer II 115. 重建序列](https://leetcode.cn/problems/ur2n8P/)

### 拓扑排序

- 时间复杂度：O(v+e)
- 空间复杂度：O(v+e)

```c++
class Solution {
public:
    bool sequenceReconstruction(vector<int>& org, vector<vector<int>>& seqs) {
        unordered_map<int, unordered_set<int>> g;
        vector<int> indeg(org.size() + 1, -1);
        for (auto& seq : seqs) {
            for (auto& n : seq) {
                if (n < 1 || n > org.size()) return false;
                if (!g.count(n)) g[n] = {};
                if (indeg[n] == -1) indeg[n] = 0;
            }
            for (int i = 1; i < seq.size(); i++) {
                int a = seq[i - 1], b = seq[i];
                if (!g[a].count(b)) {
                    g[a].insert(b);
                    indeg[b]++; // 入度
                }
            }
        }

        queue<int> q;
        int idx = 0;
        for (int i = 1; i < indeg.size(); i++) {
            if (indeg[i] == 0) {
                if (q.size() == 0 && org[idx++] == i) q.push(i);    // 唯一入度为 0 的节点，即 org[0]
                else return false;
            }
        }

        while (!q.empty()) {
            int u = q.front();
            q.pop();
            for (auto& v : g[u]) {
                if (--indeg[v] == 0) {
                    if (q.size() == 0 && org[idx++] == v) q.push(v);    // 唯一入度为 0 的节点，即 org[idx]
                    else return false;
                }
            }
        }

        return idx == org.size();
    }
};
```

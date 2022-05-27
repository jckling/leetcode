### [剑指 Offer II 113. 课程顺序](https://leetcode.cn/problems/QA2IGt/)

### 拓扑排序

- 时间复杂度：O(m+n)
- 空间复杂度：O(m+n)

```c++
class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> g(numCourses);
        vector<int> indeg(numCourses, 0);
        for (auto& p : prerequisites) {
            g[p[1]].push_back(p[0]);    // p[0] <- p[1]
            indeg[p[0]]++;
        }

        queue<int> q;
        for (int i = 0; i < numCourses; i++) {
            if (indeg[i] == 0) q.push(i);
        }

        vector<int> ans;
        while (!q.empty()) {
            int u = q.front();
            q.pop();
            ans.push_back(u);
            for (auto& v : g[u]) {
                if (--indeg[v] == 0) q.push(v);
            }
        }

        if (ans.size() != numCourses) return {};
        return ans;
    }
};
```

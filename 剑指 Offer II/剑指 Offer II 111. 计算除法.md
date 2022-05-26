### [剑指 Offer II 111. 计算除法](https://leetcode.cn/problems/vlzXQL/)

### BFS

- 时间复杂度：O(ML+Q(M+L))
  - M 表示边的数量，L 表示字符串平均长度，Q 表示询问次数
- 空间复杂度：O(NL+M)
  - N 表示点的数量

```c++
class Solution {
public:
    vector<double> calcEquation(vector<vector<string>>& equations, vector<double>& values, vector<vector<string>>& queries) {
        // 字符串 -> 数字
        int cnt = 0;
        int n = equations.size();
        unordered_map<string, int> mp;
        for (int i = 0; i < n; i++) {
            if (mp.find(equations[i][0]) == mp.end()) mp[equations[i][0]] = cnt++;
            if (mp.find(equations[i][1]) == mp.end()) mp[equations[i][1]] = cnt++;
        }

        // 构建图，边权
        vector<vector<pair<int, double>>> g(cnt);
        for (int i = 0; i < n; i++) {
            int ida = mp[equations[i][0]];
            int idb = mp[equations[i][1]];
            g[ida].push_back({idb, values[i]});         // a->b = v
            g[idb].push_back({ida, 1.0 / values[i]});   // b->a = 1/v
        }

        vector<double> res;
        for (auto& q : queries) {
            double ans = -1.0;
            if (mp.count(q[0]) && mp.count(q[1])) { // 确保节点存在
                int pa = mp[q[0]];          // 起点
                int pb = mp[q[1]];          // 终点
                if (pa == pb) ans = 1.0;    // 起点 == 终点
                else {
                    queue<int> q;
                    q.push(pa);         // 起点入队
                    vector<double> ratio(cnt, -1.0);        // 到其他节点的值
                    ratio[pa] = 1.0;    // 起点到起点 -> 1
                    while (!q.empty() && ratio[pb] < 0) {   // 终点未访问
                        int x = q.front();
                        q.pop();
                        for (auto& [y, val] : g[x]) {       // 遍历相邻节点
                            if (ratio[y] < 0) {             // 未访问
                                ratio[y] = ratio[x] * val;  // 更新值
                                q.push(y);                  // 相邻节点入队
                            }
                        }
                    }
                    ans = ratio[pb];    // 到终点的值
                }
            }
            res.push_back(ans);
        }

        return res;
    }
};
```

### [剑指 Offer II 114. 外星文字典](https://leetcode.cn/problems/Jf1JuT/)

### 拓扑排序

将每个字母看做一个节点。

- 时间复杂度：O(mn)
- 空间复杂度：O(mn)

```c++
class Solution {
public:
    string alienOrder(vector<string>& words) {
        unordered_map<char, unordered_set<char>> g;
        unordered_map<char, int> indeg;
        for (auto& word : words) {
            for (auto& c : word) {
                if (!g.count(c)) g[c] = {};
                if (!indeg.count(c)) indeg[c] = 0;
            }
        }

        for (int i = 1; i < words.size(); ++i) {
            int j = 0;
            int len = min(words[i - 1].size(), words[i].size());
            for (; j < len; j++) {
                char c1 = words[i - 1][j];
                char c2 = words[i][j];
                if (c1 != c2) {
                    if (!g[c1].count(c2)) {
                        g[c1].insert(c2);
                        indeg[c2]++;
                    }
                    break;
                }
            }
            if (j == len && words[i - 1].size() > words[i].size()) return {};   // 前一个单词是后一个单词的前缀
        }

        queue<char> q;
        for (auto& [c, cnt] : indeg) {
            if (cnt == 0) q.push(c);
        }

        string ans = "";
        while (!q.empty()) {
            char u = q.front();
            q.pop();
            ans += u;
            for (auto& v : g[u]) {
                if (--indeg[v] == 0) q.push(v);
            }
        }

        if (ans.size() != indeg.size()) return "";
        return ans;
    }
};
```

### [剑指 Offer II 109. 开密码锁](https://leetcode.cn/problems/zlDJc7/)

### BFS

双向 BFS，将访问过的密码加入集合。

- 时间复杂度：
- 空间复杂度：

```c++
class Solution {
public:
    int openLock(vector<string>& deadends, string target) {
        // 集合（去重）
        unordered_set<string> st(deadends.begin(), deadends.end());

        // 起始状态
        string s = "0000";

        // 特殊情况
        if (target == s) return 0;
        if (st.count(s) || st.count(target)) return -1;

        // 访问标记
        unordered_set<string> beginVisited;
        beginVisited.insert(s);
        unordered_set<string> endVisited;
        endVisited.insert(target);

        int step = 0;
        while (!beginVisited.empty() && !endVisited.empty()) {
            // 优先扩散小的集合
            if (beginVisited.size() > endVisited.size()) beginVisited.swap(endVisited);
            // 下一层集合
            unordered_set<string> nextVisited;
            for (string s : beginVisited) {
                st.insert(s);
                for (int i = 0; i < s.size(); i++) {    // 四位数
                    char c = s[i];
                    s[i] = c + 1 > '9' ? '0' : c + 1;
                    if (st.find(s) == st.end()) {
                        if (endVisited.find(s) != endVisited.end()) return step + 1;
                        nextVisited.insert(s);
                    }

                    s[i] = c - 1 < '0' ? '9' : c- 1;
                    if (st.find(s) == st.end()) {
                        if (endVisited.find(s) != endVisited.end()) return step + 1;
                        nextVisited.insert(s);
                    }

                    s[i] = c;
                }
            }
            beginVisited = nextVisited;
            step++;
        }

        return -1;
    }
};
```

### [剑指 Offer 38. 字符串的排列](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

### DFS

- 时间复杂度：O(n!n)
- 空间复杂度：O(n^2)

```c++
class Solution {
public:
    vector<string> permutation(string s) {
        dfs(s, 0);
        return ans;
    }
private:
    vector<string> ans;
    void dfs(string s, int idx) {
        if (idx == s.size() - 1) {
            ans.emplace_back(s);
            return;
        }

        set<int> st;
        for (int i = idx; i < s.size(); i++) {
            if(st.find(s[i]) != st.end()) continue;

            st.insert(s[i]);
            swap(s[i], s[idx]);
            dfs(s, idx + 1);
            swap(s[i], s[idx]);
        }
    }
};
```

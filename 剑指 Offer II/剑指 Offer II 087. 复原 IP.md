### [剑指 Offer II 087. 复原 IP](https://leetcode.cn/problems/0on3uN/)

### DFS

- 时间复杂度：$O(3^4 \times |s|)$
	- 每层节点最多 3 个分支，树最多 4 层
- 空间复杂度：O(h)
	- 树的高度 4

```c++
class Solution {
public:
    vector<string> restoreIpAddresses(string s) {
        dfs(s, 0, 0);
        return ans;
    }
private:
    vector<string> ans;
    void dfs(string& s, int idx, int cnt) {
        if (cnt == 3) {
            if (isValid(s, idx, s.size() - 1)) ans.push_back(s);
            return;
        }

        for (int i = idx; i < s.size(); i++) {
            if (isValid(s, idx, i)) {
                s.insert(s.begin() + i + 1, '.');
                dfs(s, i + 2, cnt + 1);
                s.erase(s.begin() + i + 1);
            }
        }
    }
    bool isValid(string& s, int l, int r) {
        if (l > r || s[l] =='0' && l != r) return false;
        int n = 0;
        for (int i = l; i <= r; i++) {
            if (s[i] > '9' || s[i] < '0') return false;
            n = n * 10 + (s[i] - '0');
            if (n > 255) return false;
        }
        return true;
    }
};
```

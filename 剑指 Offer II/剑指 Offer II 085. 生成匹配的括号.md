### [剑指 Offer II 085. 生成匹配的括号](https://leetcode.cn/problems/IDBivT/)

### DFS

- 时间复杂度：$O(\frac{4^n}{\sqrt{n}})$
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        dfs("", n, n);
        return ans;
    }
private:
    vector<string> ans;
    void dfs (string s, int l, int r) {
        if (l ==0 && r == 0) {
            ans.push_back(s);
            return;
        }
        if (l > 0) dfs(s + '(', l - 1, r);
        if (r > l) dfs(s + ')', l, r - 1);
    }
};
```

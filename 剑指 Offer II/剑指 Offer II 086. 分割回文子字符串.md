### [剑指 Offer II 086. 分割回文子字符串](https://leetcode.cn/problems/M99OJA/)

### DFS

- 时间复杂度：$O(n*2^n)$
  - 判断回文 O(n)，每个位置可拆分可不拆分 O(2^n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<vector<string>> partition(string s) {
        dfs(s, 0);
        return ans;
    }
private:
    vector<vector<string>> ans;
    vector<string> tmp;
    void dfs(string& s, int idx) {
        if (idx >= s.size()) {
            ans.push_back(tmp);
            return;
        }

        for (int i = idx; i < s.size(); i++) {
            if (!isPalindrome(s, idx, i)) continue;
            string sub = s.substr(idx, i - idx + 1);
            tmp.push_back(sub);
            dfs(s, i + 1);
            tmp.pop_back();
        }
    }
    bool isPalindrome(string& s, int l, int r) {
        while (l < r) {
            if (s[l] != s[r]) return false;
            l++;
            r--;
        }
        return true;
    }
};
```

### [剑指 Offer II 032. 有效的变位词](https://leetcode.cn/problems/dKk3P7/)

### 遍历

- 时间复杂度：O(m+n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s == t) return false;
        
        vector<int> ss(26);
        for (auto& c : s) ss[c - 'a']++;
        vector<int> st(26);
        for (auto& c : t) st[c - 'a']++;
        return ss == st;
    }
};
```

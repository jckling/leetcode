### [剑指 Offer II 015. 字符串中的所有变位词](https://leetcode.cn/problems/VabMRr/)

### 滑动窗口

- 时间复杂度：O(m+n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        if (s.size() < p.size()) return {};

        vector<int> sp(26, 0);
        vector<int> ss(26, 0);
        for (int i = 0; i < p.size(); i++) {
            ss[s[i] - 'a']++;
            sp[p[i] - 'a']++;
        }

        vector<int> ans;
        if (ss == sp) ans.push_back(0);
        for (int l = 0, r = p.size(); r < s.size(); l++, r++) {
            ss[s[l] - 'a']--;
            ss[s[r] - 'a']++;
            if (ss == sp) ans.push_back(l + 1);
        }

        return ans;
    }
};
```

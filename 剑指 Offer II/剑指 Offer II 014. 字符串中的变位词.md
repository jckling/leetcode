### [剑指 Offer II 014. 字符串中的变位词](https://leetcode.cn/problems/MPnaiL/)

### 滑动窗口

- 时间复杂度：O(m+n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    bool checkInclusion(string s1, string s2) {
        if (s1.size() > s2.size()) return false;

        vector<int> cnt1(26, 0);
        for (auto c : s1) cnt1[c - 'a']++;

        vector<int> cnt2(26, 0);
        for (int i = 0; i < s1.size(); i++) {
            cnt2[s2[i] - 'a']++;
        }

        if (cnt1 == cnt2) return true;
        for (int l = 0, r = s1.size(); r < s2.size(); l++, r++) {
            cnt2[s2[l] - 'a']--;
            cnt2[s2[r] - 'a']++;
            if (cnt1 == cnt2) return true;
        }
        return false;
    }
};
```

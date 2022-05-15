### [剑指 Offer II 016. 不含重复字符的最长子字符串](https://leetcode.cn/problems/wtcaE1/)

### 滑动窗口

- 时间复杂度：O(n)
- 空间复杂度：O(e)

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if (s.size() == 0) return 0;

        int len = 0;
        unordered_set<char> st;
        for (int l = -1, r = 0; r < s.size(); r++) {
            while (st.count(s[r])) st.erase(s[++l]);
            st.insert(s[r]);
            len = max(len, r - l);
        }

        return len;
    }
};
```

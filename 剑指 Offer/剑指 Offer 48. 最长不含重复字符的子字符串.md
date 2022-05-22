### [剑指 Offer 48. 最长不含重复字符的子字符串](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

### 滑动窗口

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int ans = 0;
        unordered_map<char, int> mp;
        for (int i = -1, j = 0; j < s.size(); j++) {
            if (mp.find(s[j]) != mp.end()) i = max(i, mp[s[j]]);
            mp[s[j]] = j;
            ans = max(ans, j - i);
        }
        return ans;
    }
};
```

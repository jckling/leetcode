### [剑指 Offer II 017. 含有所有字符的最短字符串](https://leetcode.cn/problems/M1oyTv/)

### 滑动窗口

- 时间复杂度：O(n)
- 空间复杂度：O(k)

```c++
class Solution {
public:
    string minWindow(string s, string t) {
        if (s.size() < t.size()) return "";
        if (s.size() == 1 && t.size() == 1) return s == t ? s : "";

        // 统计字母出现频率
        vector<int> cnt(128, 0);
        for (auto c : t) cnt[c]++;
        for (int i = 0; i < cnt.size(); i++) {
            if (cnt[i] == 0) cnt[i] = INT_MIN;
        }

        int tot = t.size(); // 待匹配数量
        int start = 0, len = INT_MAX;
        for (int l = 0, r = 0; l < s.size(); l++) {
            // 右边界
            while (r < s.size() && tot > 0) {
                char c = s[r];
                if (cnt[c] != INT_MIN) {
                    if (cnt[c] > 0) tot--;
                    cnt[c]--;
                }
                r++;
            }
            // 匹配完毕
            if (tot == 0 && r - l < len) {
                len = r - l;
                start = l;
            }
            // 左边界
            char c = s[l];
            if (cnt[c] != INT_MIN) {
                if (cnt[c] == 0) tot++;
                cnt[c]++;
            }
        }

        return len < INT_MAX ? s.substr(start, len) : "";
    }
};
```

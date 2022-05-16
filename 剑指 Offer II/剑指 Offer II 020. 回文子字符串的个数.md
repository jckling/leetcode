### [剑指 Offer II 020. 回文子字符串的个数](https://leetcode.cn/problems/a7VOhD/)

### 中心扩展

- 时间复杂度：O(n^2)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int countSubstrings(string s) {
        int n = s.size();
        int cnt = 0;

        // 一个字母为中心，两个字母为中心
        for (int i = 0; i < 2 * n - 1; i++) {
            int l = i / 2, r = i / 2 + i % 2;
            // 中心扩展
            while (l >= 0 && r < n && s[l] == s[r]) {
                l--;
                r++
                cnt++;
            }
        }
        return cnt;
    }
};
```

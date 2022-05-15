### [剑指 Offer II 005. 单词长度的最大乘积](https://leetcode.cn/problems/aseY1I/)

### 位运算

- 时间复杂度：O((m+n)*n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int maxProduct(vector<string>& words) {
        // 字母出现情况 -> 单词长度
        unordered_map<int, int> mp;
        for (int i = 0; i < words.size(); i++) {
            // 用 mask 记录字母出现情况
            int mask = 0;
            for (char c : words[i]) mask |= 1 << (c - 'a');
            
            // 已出现过，保留单词长度更长的
            if (mp.count(mask)) {
                int imax = max(mp[mask], words[i].size());
                mp[mask] = imax;
            }
            else mp[mask] = words[i].size();
        }

        int ans = 0;
        for (auto& x : mp) {
            for (auto& y : mp) {
                // 字母不重复
                if ((x.first & y.first) == 0) {
                    ans = max(ans, x.second * y.second);
                }
            }
        }

        return ans;
    }
private:
    int max (int a, int b) { return a > b ? a : b; }
};
```

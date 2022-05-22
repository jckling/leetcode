### [剑指 Offer 50. 第一个只出现一次的字符](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

### 哈希表

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    char firstUniqChar(string s) {
        unordered_map<char, int> mp;
        for (auto& c : s) mp[c]++;
        for (auto& c : s) {
            if (mp[c] == 1) return c;
        }
        return ' ';
    }
};
```

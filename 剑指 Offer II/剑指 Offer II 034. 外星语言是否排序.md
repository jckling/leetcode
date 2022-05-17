### [剑指 Offer II 034. 外星语言是否排序](https://leetcode.cn/problems/lwyVBB/)

### 哈希表

- 时间复杂度：O(mn)
- 空间复杂度：O(c)

```c++
class Solution {
public:
    bool isAlienSorted(vector<string>& words, string order) {
        if (words.size() == 0 || words.size() == 1) return true;

        unordered_map<char, int> mp;
        for (int i = 0; i < order.size(); i++) mp[order[i]] = i;

        for (int i = 1; i < words.size(); i++) {
            string w1 = words[i - 1];
            string w2 = words[i];
            int len1 = w1.size(), len2 = w2.size();
            for (int j = 0; j < max(len1, len2); j++) {
                int idx1 = j >= len1 ? -1 : mp[w1[j]];
                int idx2 = j >= len2 ? -1 : mp[w2[j]];
                if (idx1 > idx2) return false;
                if (idx1 < idx2) break;
            }
        }

        return true;
    }
};
```

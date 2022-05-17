### [剑指 Offer II 033. 变位词组](https://leetcode.cn/problems/sfvd7V/)

### 哈希表

- 时间复杂度：O(nklog(k))
	- n 表示字符串数量，k 表示最大的字符串长度
- 空间复杂度：O(nk)

```c++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> mp;
        for (auto key : strs) {
            string s = key;
            sort(key.begin(), key.end());
            mp[key].emplace_back(s);
        }

        vector<vector<string>> ans;
        for (auto p : mp) ans.emplace_back(p.second);
        return ans;
    }
};
```

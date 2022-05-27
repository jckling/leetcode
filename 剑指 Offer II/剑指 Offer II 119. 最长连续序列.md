### [剑指 Offer II 119. 最长连续序列](https://leetcode.cn/problems/WhsWhI/)

### 哈希表

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_set<int> st(nums.begin(), nums.end());
        int ans = 0;
        for (auto& num : st) {
            if (!st.count(num - 1)) {
                int cur = num;
                int len = 1;
                while (st.count(cur + 1)) {
                    cur++;
                    len++;
                }
                ans = max(ans, len);
                if (ans >= st.size() / 2) break;
            }
        }
        return ans;
    }
};
```

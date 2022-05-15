### [剑指 Offer II 011. 0 和 1 个数相同的子数组](https://leetcode.cn/problems/A1NYOS/)

### 哈希表 + 前缀和

遇到 0 减一，遇到 1 加一：求最长的连续子数组，其元素和为 0

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int findMaxLength(vector<int>& nums) {
        int len = 0;
        int pre = 0;    // 前缀和

        // 存储前缀和出现的下标
        unordered_map<int, int> mp;
        // 边界
        mp[0] = -1;

        for (int i = 0; i < nums.size(); i++) {
            pre += nums[i] == 0 ? -1 : 1;
            // 出现过前缀和为 pre 的，相减即为 0
            if (mp.count(pre)) len = max(len, i - mp[pre]);
            else mp[pre] = i;
        }

        return len;
    }
};
```

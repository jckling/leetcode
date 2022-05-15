### [剑指 Offer II 010. 和为 k 的子数组](https://leetcode.cn/problems/QTMn0o/)

### 哈希表 + 前缀和

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int cnt = 0;
        int pre = 0;    // 前缀和

        // 统计相同前缀和的数量
        unordered_map<int, int> mp;
        // 边界，前缀和为 0 出现一次
        // nums = [3,...], k = 3，和 nums = [1, 1, 1,...], k = 3
        mp[0] = 1;

        for (auto n : nums) {
            pre += n;
            // 找到一个前缀和，相减为 k
            if (mp.find(pre - k) != mp.end()) cnt += mp[pre - k];
            mp[pre]++;
        }
        return cnt;
    }
};
```

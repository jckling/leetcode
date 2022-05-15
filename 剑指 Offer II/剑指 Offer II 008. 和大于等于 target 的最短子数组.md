### [剑指 Offer II 008. 和大于等于 target 的最短子数组](https://leetcode.cn/problems/2VG8Kg/)

### 滑动窗口

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int ans = INT_MAX;
        int l = -1;
        int sum = 0;
        for (int r = 0; r < nums.size(); r++) {
            sum += nums[r];
            if (sum < target) continue;
            while (sum >= target) {
                sum -= nums[++l];
            }
            ans = min(ans, r - l + 1);
        }

        return ans == INT_MAX ? 0 : ans;
    }
};
```

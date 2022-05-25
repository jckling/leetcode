### [剑指 Offer II 104. 排列的数目](https://leetcode.cn/problems/D0F0SV/)

### 动态规划

爬楼梯：楼梯的阶数为 `target`，每次可以走的步数为 `nums[i]`，一共有多少种走法？

- 时间复杂度：$O(n*target)$
- 空间复杂度：O(target)

```c++
class Solution {
public:
    int combinationSum4(vector<int>& nums, int target) {
        vector<int> dp(target + 1);
        dp[0] = 1;

        for (int i = 1; i <= target; i++) {
            for (int& num : nums) {
                // 防止中间溢出
                if (i >= num && dp[i - num] < INT_MAX - dp[i]) {
                    dp[i] += dp[i - num];
                }
            }
        }

        return dp[target];
    }
};
```

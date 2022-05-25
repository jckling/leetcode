### [剑指 Offer II 102. 加减的目标值](https://leetcode.cn/problems/YaVDxD/)

### 动态规划

`dp[i][j]` 表示前 i 个元素有多少个目标和为 j 的子集。

- 时间复杂度：O(n\*neg)
- 空间复杂度：O(n\*neg)
  - neg 表示负数的数量

```c++
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int target) {
        // sum - 2*neg = target
        int sum = accumulate(nums.begin(), nums.end(), 0);
        int diff = sum - target;
        if (diff < 0 || diff % 2 != 0) return false;

        int n = nums.size(), neg = diff / 2;
        vector<vector<int>> dp(n + 1, vector<int>(neg + 1));
        dp[0][0] = 1;

        for (int i = 1; i <= n; i++) {
            int num = nums[i - 1];
            for (int j = 0; j <= neg; j++) {
                dp[i][j] = dp[i - 1][j];    // 不选 num
                if (j >= num) dp[i][j] += dp[i - 1][j - num];  // 选 num
            }
        }

        return dp[n][neg];
    }
};
```

### [剑指 Offer II 103. 最少的硬币数目](https://leetcode.cn/problems/gaM7Ch/)

### 动态规划

`dp[i]` 表示凑成金额 i 用的最少硬币数量。

- 时间复杂度：O(Sn)
  - S 金额，n 硬币面额
- 空间复杂度：O(S)

```c++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        if (coins.size() == 0) return -1;
        if (amount == 0) return 0;

        int imax = amount + 1;
        vector<int> dp(imax, imax);
        dp[0] = 0;
        for (int i = 1; i <= amount; i++) {
            for (int j = 0; j < coins.size(); j++) {
                if (coins[j] <= i) dp[i] = min(dp[i], dp[i - coins[j]] + 1);
            }
        }

        return dp[amount] == imax ? -1 : dp[amount];
    }
};
```

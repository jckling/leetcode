### [剑指 Offer 60. n 个骰子的点数](https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/)

### 动态规划

- 时间复杂度：O(n^2)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<double> dicesProbability(int n) {
        vector<double> dp(6, 1.0 / 6.0);    //  第一轮
        for (int i = 2; i <= n; i++) {      // 第二轮至第 n 轮
            vector<double> tmp(5 * i + 1, 0);       // 本轮概率
            for (int j = 0; j < dp.size(); j++) {   // 上一轮的和值 j + k
                for (int k = 0; k < 6; k++) {
                    tmp[j + k] += dp[j] / 6.0;      // 基于上一轮的和值，在本轮投出 1-6 中某个点数的概率应该是：上一轮概率*(1/6)
                }
            }
            dp = tmp;
        }
        return dp;
    }
};
```

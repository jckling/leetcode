### [剑指 Offer 49. 丑数](https://leetcode-cn.com/problems/chou-shu-lcof/)

### 动态规划

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int nthUglyNumber(int n) {        
        int dp[n];
        dp[0] = 1;  // 第 1 个丑数为 1

        int a = 0, b = 0, c = 0;    // 2, 3, 5
        for (int i = 1; i < n; i++) {
            int n2 = dp[a] * 2, n3 = dp[b] * 3, n5 = dp[c] * 5;
            dp[i] = min(min(n2, n3), n5);
            if (dp[i] == n2) a++;
            if (dp[i] == n3) b++;
            if (dp[i] == n5) c++;
        }

        return dp[n - 1];
    }
};
```

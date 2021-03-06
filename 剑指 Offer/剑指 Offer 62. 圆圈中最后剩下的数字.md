### [剑指 Offer 62. 圆圈中最后剩下的数字](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)

### 动态规划

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int lastRemaining(int n, int m) {
        // [1, m] 问题的解恒为 0，因此 dp[1] = 0
        int x = 0; 

        // [i, m] 问题
        for (int i = 2; i <= n; i++) {
            x = (x + m) % i;    // dp[i] = (dp[i − 1] + m) % i
        }

        // [n, m] 问题
        return x;
    }
};
```

### [剑指 Offer 10- II. 青蛙跳台阶问题](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

### 动态规划

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int numWays(int n) {
        int mod = 1e9 + 7;
        int a = 0, b = 1;
        for (int i = 1; i <= n; i++) {
            int c = (a + b) % mod;
            a = b;
            b = c;
        }
        return b;
    }
};
```

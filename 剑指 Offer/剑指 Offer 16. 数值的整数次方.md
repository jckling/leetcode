### [剑指 Offer 16. 数值的整数次方](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

### 快速幂

- 时间复杂度：O(logn)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    double myPow(double x, int n) {
        if (x == 0.0 || x == 1.0) return x;

        long b = n;
        double res = 1.0;
        if (b < 0) {
            x = 1.0 / x;
            b = -b;
        }

        // 快速幂
        while (b > 0) {
            if ((b & 1) == 1) res *= x;
            x *= x;
            b >>= 1;
        }

        return res;
    }
};
```

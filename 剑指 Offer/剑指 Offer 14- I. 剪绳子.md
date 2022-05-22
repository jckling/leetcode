### [剑指 Offer 14- I. 剪绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)

### 数学

- 时间复杂度：O(1)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int cuttingRope(int n) {
        if (n < = 3) return n - 1;
        int a = n / 3, r = b % 3;
        if (b == 0) return pow(3, a);
        if (b == 1) return pow(3, a - 1) * 4;
        return pow(3, a) * 2;
    }
};
```

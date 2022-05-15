### [剑指 Offer II 001. 整数除法](https://leetcode.cn/problems/xoh6Oh/)

### 数学

- 时间复杂度：O(logn)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int divide(int a, int b) {
        if (a == 0) return 0;
        if (b == 1) return a;
        if (b == -1) return a > INT_MIN ? -a : INT_MAX;

        // 结果正负
        int sign = -1;
        if ((a < 0 && b < 0) || (a > 0 && b > 0)) sign = 1;

        // 转换为负数
        a = a > 0 ? -a : a;
        b = b > 0 ? -b : b;

        // 倍增乘法
        int ans = 0;
        while (a <= b) {
            int tmp = b;
            int cnt = 1;
            while (tmp >= a - tmp) {
                tmp += tmp;
                cnt += cnt;
            }
            a -= tmp;
            ans += cnt;
        }

        return sign == -1 ? -ans : ans;
    }
};
```

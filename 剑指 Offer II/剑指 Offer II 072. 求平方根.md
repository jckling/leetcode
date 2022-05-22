### [剑指 Offer II 072. 求平方根](https://leetcode.cn/problems/jJ0w9p/)

### 二分

- 时间复杂度：O(logx)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int mySqrt(int x) {
        int ans = -1;
        int l = 0, r = x;
        while (l <= r) {
            int m = l + (r - l) / 2;
            if ((long) m * m <= x) {
                ans = m;
                l = m + 1;
            }
            else r = m - 1;
        }
        return ans;
    }
};
```

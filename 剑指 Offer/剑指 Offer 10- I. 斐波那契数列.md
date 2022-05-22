### [剑指 Offer 10- I. 斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

### 动态规划

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int fib(int n) {
        if (n == 0 || n == 1) return n;

        int mod = 1e9 + 7;
        int a = 0, b = 1;
        for (int i = 2; i <= n; i++) {
            int c = (a + b) % mod;
            a = b;
            b = c;
        }

        return b;
    }
};
```

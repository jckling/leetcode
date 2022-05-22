### [剑指 Offer 64. 求 1 + 2 + … + n](https://leetcode-cn.com/problems/qiu-12n-lcof/)

### 短路求值

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int sumNums(int n) {
        n > 1 && (n += sumNums(n - 1));
        return n;
    }
};
```

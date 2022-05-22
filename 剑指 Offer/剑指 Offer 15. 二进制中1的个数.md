### [剑指 Offer 15. 二进制中1的个数](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)

### 位运算

- 时间复杂度：O(m)
    - m 表示二进制中 1 的个数
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int cnt = 0;
        while (n) {
            cnt++;
            n &= (n - 1);
        }
        return cnt;
    }
};
```

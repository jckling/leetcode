### [剑指 Offer 65. 不用加减乘除做加法](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/)

### 位运算

- 时间复杂度：O(1)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int add(int a, int b) {
        while (b != 0) {
            int c = (unsigned int) (a & b) << 1;    // 进位
            a ^= b; // 非进位和
            b = c;
        }
        return a;
    }
};
```

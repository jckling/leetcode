### [剑指 Offer 56 - I. 数组中数字出现的次数](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)

### 数学

![](https://pic.leetcode-cn.com/1614836837-oygHyk-Picture2.png)

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    vector<int> singleNumbers(vector<int>& nums) {
        // 遍历异或，得到 A xor B
        int n = 0;
        for (auto& num : nums) n ^= num;

        // 循环左移，得到二进制从右往左第一个 1
        int m = 1;
        while ((n & m) == 0) m <<= 1;

        // 分组
        int x = 0, y = 0;
        for (auto& num : nums) {
            if (num & m) x ^= num;  // num & m != 0
            else y ^= num;          // num & m == 0
        }
        
        return {x, y};
    }
};
```

### [剑指 Offer 56 - II. 数组中数字出现的次数 II](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

### 有限状态自动机

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ones = 0, twos = 0;
        for (auto& num : nums) {
            ones = ones ^ num & ~twos;
            twos = twos ^ num & ~ones;
        }
        return ones;
    }
};
```

### 遍历

计数求余

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        // 1. 统计每一位的 1 总数
        vector<int> cnt(32, 0);
        for (auto& num : nums) {
            for (int i = 0; i < 32; i++) {
                cnt[i] += num & 1;      // 第 i 位的 1 
                num >>= 1;              // 第 i + 1 位
            }
        }

        // 2. 对 3 求余
        int ans = 0;
        for (int i = 31; i >= 0; i--) {
            ans <<= 1;          // 左移乘以 2
            ans |= cnt[i] % 3;  // 第 i 位
        }

        // 3. 返回结果
        return ans;
    }
};
```

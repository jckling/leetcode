### [剑指 Offer II 004. 只出现一次的数字 ](https://leetcode.cn/problems/WGki4K/)

### 遍历

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        vector<int> cnt(32);
        for (auto num : nums) {
            for (int i = 0; i < 32; i++) {
                cnt[i] += num & 1;
                num >>= 1;
            }
        }

        int ans = 0;
        for (int i = 31; i >= 0; i--) {
            ans <<= 1;
            ans |= cnt[i] % 3;
        }

        return ans;
    }
};
```

### 自动机

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ones = 0, twos = 0;
        for (auto num : nums) {
            ones = ones ^ num & ~twos;
            twos = twos ^ num & ~ones;
        }
        return ones;
    }
};
```

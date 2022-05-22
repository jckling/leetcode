### [剑指 Offer II 070. 排序数组中只出现一次的数字](https://leetcode.cn/problems/skFtm2/)

### 二分

成对元素中的第一个下标是偶数，第二个下标是奇数。

- 时间复杂度：O(logn)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        int l = 0, r = nums.size() - 1;
        while (l < r) {
            int m = (l + r) / 2;
            if (m % 2 == 0) {
                if (nums[m] == nums[m + 1]) l = m + 1;  // 成对
                else r = m;
            }
            else {
                if (nums[m - 1] == nums[m]) l = m + 1;  // 成对
                else r = m;
            }
        }
        return nums[l];
    }
};
```

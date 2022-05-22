### [剑指 Offer 53 - II. 0～n-1 中缺失的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

### 二分

索引与值对应

- 时间复杂度：O(log n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int i = 0, j = nums.size() - 1;
        while (i <= j) {
            int m = (i + j) / 2;
            if (nums[m] == m) i = m + 1;
            else j = m - 1;
        }

        return i;
    }
};
```

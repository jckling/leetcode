### [剑指 Offer 53 - I. 在排序数组中查找数字 I](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

### 二分

- 时间复杂度：O(logn)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        // 右边界
        int l = 0, r = nums.size() - 1;
        while (l <= r) {
            int m = (l + r) / 2;
            if (nums[m] <= target) l = m + 1;
            else r = m - 1;
        }
        int right = l;  // 大于 target 的第一个数字

        // 提前返回
        if (r >= 0 && nums[r] != target) return 0;

        // 左边界
        l = 0, r = nums.size() - 1;
        while (l <= r) {
            int m = (l + r) / 2;
            if (nums[m] >= target) r = m - 1;
            else l = m + 1;
        }
        int left = r;   // 小于 target 的第一个数字

        return right - left - 1;
    }
};
```

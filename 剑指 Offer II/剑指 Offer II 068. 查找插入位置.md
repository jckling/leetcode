### [剑指 Offer II 068. 查找插入位置](https://leetcode.cn/problems/N6YdxV/)

### 二分

- 时间复杂度：O(logn)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int l = 0, r = nums.size() - 1;
        while (l <= r) {
            int m = (l + r) / 2;
            if (nums[m] < target) l = m + 1;
            else if (nums[m] > target) r = m - 1;
            else return m;
        }
        return l;
    }
};
```

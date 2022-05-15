### [剑指 Offer II 009. 乘积小于 K 的子数组](https://leetcode.cn/problems/ZVAVXX/)

### 滑动窗口

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int numSubarrayProductLessThanK(vector<int>& nums, int k) {
        int cnt = 0;
        int sum = 1;
        for (int l = 0, r = 0; r < nums.size(); r++) {
            sum *= nums[r];
            while (l <= r && sum >= k) {
                sum /= nums[l++];
            }
            // 窗口内的连续子数组个数
            cnt += r - l + 1;
        }

        return cnt;
    }
};
```

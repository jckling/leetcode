### [剑指 Offer II 012. 左右两边子数组的和相等](https://leetcode.cn/problems/tvdfij/)

### 前缀和

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int pivotIndex(vector<int>& nums) {
        int total = accumulate(nums.begin(), nums.end(), 0);
        int sum = 0;    // 左区间和
        
        for (int i = 0; i < nums.size(); i++) {
            // total- nums[i] - sum = sum   // 右区间和 = 左区间和
            if (2 * sum + nums[i] == total) return i;   // 不包括中心
            sum += nums[i];
        }

        return -1;
    }
};
```

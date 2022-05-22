### [剑指 Offer 57. 和为 s 的两个数字](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

### 双指针

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int i = 0, j = nums.size() - 1;
        while(i < j) {
            if(nums[i] + nums[j] < target) i++;
            else if(nums[i] + nums[j] >  target) j--;
            else return {nums[i], nums[j]};
        }
        return {};
    }
};
```

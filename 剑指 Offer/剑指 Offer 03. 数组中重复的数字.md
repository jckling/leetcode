### [剑指 Offer 03. 数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

### 原地操作

`索引 -> 数字`，将数字放到对应位置上

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        int i = 0;
        while(i < nums.size()) {
            if(nums[i] == i) {  // 索引与值对应，一对多
                i++;
                continue;
            }
            if(nums[i] == nums[nums[i]]) return nums[i];
            swap(nums[i], nums[nums[i]]);
        }

        return -1;
    }
};
```

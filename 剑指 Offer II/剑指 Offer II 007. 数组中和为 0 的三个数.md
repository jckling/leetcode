### [剑指 Offer II 007. 数组中和为 0 的三个数](https://leetcode.cn/problems/1fGaJU/)

### 双指针

排序 + 固定一位 + 双指针 + 去重

- 时间复杂度：O(n^2)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> ans;
        if (nums.size() < 3) return ans;

        sort(nums.begin(), nums.end());
        for (int k = 0; k < nums.size(); k++) {
            if (nums[k] > 0) break;
            if (k > 0 && nums[k] == nums[k - 1]) continue;
            // 双指针
            int i = k + 1, j = nums.size() - 1;
            while (i < j) {
                if (nums[k] + nums[i] + nums[j] < 0) i++;
                else if (nums[k] + nums[i] + nums[j] > 0) j--;
                else {
                    ans.push_back({nums[k], nums[i], nums[j]});
                    i++;
                    j--;
                    // 去重
                    while (i < j && nums[i] == nums[i - 1]) i++;
                    while (i < j && nums[j] == nums[j + 1]) j--;
                }
            } 
        }

        return ans;
    }
};
```


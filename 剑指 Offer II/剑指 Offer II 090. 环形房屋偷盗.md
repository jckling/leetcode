### [剑指 Offer II 090. 环形房屋偷盗](https://leetcode.cn/problems/PzWKhm/)

### 动态规划

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.size() == 1) return nums[0];
        if (nums.size() == 2) return max(nums[0], nums[1]);

        int res1 = robHouses(nums, 0, nums.size() - 2); // 第一间，最后一间不偷
        int res2 = robHouses(nums, 1, nums.size() - 1); // 第二间，最后一间
        return max(res1, res2);
    }
private:
    int robHouses(vector<int>& nums, int start, int end) {
        int a = 0, b = 0;
        for (int i = start; i <= end; i++) {
            int c = max(a + nums[i], b);
            a = b;
            b = c;
        }
        return b;
    }
};
```

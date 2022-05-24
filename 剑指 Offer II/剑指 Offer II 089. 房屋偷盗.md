### [剑指 Offer II 089. 房屋偷盗](https://leetcode.cn/problems/Gu0c2T/)

### 动态规划

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int rob(vector<int>& nums) {
        int a = 0, b = nums[0];
        for (int i = 1; i < nums.size(); i++) {
            int c = max(a + nums[i], b);
            a = b;
            b = c;
        }
        return b;
    }
};
```

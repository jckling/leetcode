### [剑指 Offer II 100. 三角形中最小路径之和](https://leetcode.cn/problems/IlPe0q/)

### 动态规划

从下往上计算

- 时间复杂度：O(n^2)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        vector<int> dp(triangle.size() + 1);
        for (int i = triangle.size() - 1; i >= 0; i--) {
            for (int j = 0; j < triangle[i].size(); j++) {
                dp[j] = min(dp[j], dp[j + 1]) + triangle[i][j];
            }
        }
        return dp[0];
    }
};
```

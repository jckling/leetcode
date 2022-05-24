### [剑指 Offer II 088. 爬楼梯的最少成本](https://leetcode.cn/problems/GzCJIP/)

### 动态规划

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        int a = 0, b = 0;   // 走两步，走一步
        for (int i = 2; i <= cost.size(); i++) {
            int c = min(a + cost[i - 2], b + cost[i - 1]);
            a = b;
            b = c;
        }
        return b;
    }
};
```

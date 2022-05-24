### [剑指 Offer II 091. 粉刷房子](https://leetcode.cn/problems/JEj789/)

### 动态规划

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int minCost(vector<vector<int>>& costs) {
        int a = costs[0][0], b = costs[0][1], c = costs[0][2];
        for (int i = 1; i < costs.size(); i++) {
            int aa = min(b, c) + costs[i][0];
            int bb = min(a, c) + costs[i][1];
            int cc = min(a, b) + costs[i][2];
            a = aa;
            b = bb;
            c = cc;
        }
        return min(a, min(b, c));
    }
};
```

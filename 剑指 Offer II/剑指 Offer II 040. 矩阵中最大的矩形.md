### [剑指 Offer II 040. 矩阵中最大的矩形](https://leetcode.cn/problems/PLYXKQ/)

### 单调栈

- 时间复杂度：O(mn)
- 空间复杂度：O(mn)

```c++
class Solution {
public:
    int maximalRectangle(vector<string>& matrix) {
        int m = matrix.size(), n = m ? matrix[0].size() : 0;

        vector<int> heights(n + 2, 0);  // 左右哨兵
        stack<int> stk; // 单调栈
        int ans = 0;

        for (int i = 0; i < m; i++) {
            // 重要！！每轮清空
            while(!stk.empty()) stk.pop();

            // 更新高度
            for (int j = 0; j <= n; j++) {
                if (j < n) {
                    if (matrix[i][j] == '1') heights[j] += 1;
                    else heights[j] = 0;
                }

                // 每次判断新的栈顶是否高于当前元素
                while (!stk.empty() && heights[j] < heights[stk.top()]) {
                    int h = heights[stk.top()];
                    stk.pop();
                    int l = stk.empty() ? -1 : stk.top();
                    int r = j;
                    int area = (r - l - 1) * h;
                    ans = max(ans, area);
                }
                stk.push(j);
            }
        }

        return ans;
    }
};
```

### [剑指 Offer II 039. 直方图最大矩形面积](https://leetcode.cn/problems/0ynMMM/)

### 单调栈

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        // 哨兵
        heights.insert(heights.begin(), 0);
        heights.push_back(0);

        // 单调栈
        stack<int> stk;
        stk.push(0);    // 第一个元素下标入栈

        int ans = 0;
        for (int i = 1; i < heights.size(); i++) {
            while (heights[i] < heights[stk.top()]) {   // 栈顶为右边界
                int mid = stk.top();
                stk.pop();
                int w = i - stk.top() - 1;
                int h = heights[mid];
                ans = max(ans, w * h);
            }
            stk.push(i);
        }

        return ans;
    }
};
```

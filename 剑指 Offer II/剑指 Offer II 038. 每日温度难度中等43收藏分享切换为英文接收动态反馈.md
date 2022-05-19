### [剑指 Offer II 038. 每日温度](https://leetcode.cn/problems/iIQa4I/)

### 单调栈

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        int n = temperatures.size();
        vector<int> ans(n, 0);

        // 单调栈
        stack<int> stk;

        // 单调递减，存储下标
        for (int i = 0; i < n; i++) {
            while (!stk.empty() && temperatures[i] > temperatures[stk.top()]) {
                int t = stk.top();
                stk.pop();
                ans[t] = i - t; // 距离
            }
            stk.push(i);
        }

        return ans;
    }
};
```

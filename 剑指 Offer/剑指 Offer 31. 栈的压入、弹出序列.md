### [剑指 Offer 31. 栈的压入、弹出序列](https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/)

### 模拟

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        stack<int> stk;
        int i = 0;
        for (auto& num : pushed) {
            stk.push(num);
            while (!stk.empty() && stk.top() == popped[i]) {
                stk.pop();
                i++;
            }
        }

        return stk.empty();
    }
};
```

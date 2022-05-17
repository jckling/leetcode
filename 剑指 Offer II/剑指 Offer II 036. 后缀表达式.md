### [剑指 Offer II 036. 后缀表达式](https://leetcode.cn/problems/8Zf90G/)


### 栈

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> ops;
        for (auto& t : tokens) {
            if (t == "+" || t == "-" || t == "*" || t == "/") {
                int b = ops.top(); ops.pop();
                int a = ops.top(); ops.pop();
                if (t == "+") ops.push(a + b);
                if (t == "-") ops.push(a - b);
                if (t == "*") ops.push(a * b);
                if (t == "/") ops.push(a / b);
            }
            else ops.push(stoi(t));
        }
        return ops.top();
    }
};
```

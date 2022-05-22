### [剑指 Offer 58 - I. 翻转单词顺序](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/)

### 栈

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    string reverseWords(string s) {
        stack<string> stk;
        string tmp = "";
        for (auto& c : s) {
            if (c == ' ') {
                if (tmp != "")stk.push(tmp);
                tmp = "";
            }
            else tmp += c;
        }

        while (!stk.empty()) {
            if (tmp != "") tmp += " ";
            tmp += stk.top();
            stk.pop();
        }

        return tmp;
    }
};
```

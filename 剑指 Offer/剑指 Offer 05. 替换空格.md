### [剑指 Offer 05. 替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

### 遍历

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    string replaceSpace(string s) {
        string ss = "";
        for (auto& c : s) {
            if (c == ' ') ss += "%20";
            else ss += c;
        }
        return ss;
    }
};
```

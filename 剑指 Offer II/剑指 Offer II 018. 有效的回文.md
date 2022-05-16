### [剑指 Offer II 018. 有效的回文](https://leetcode.cn/problems/XltzEq/)

### 双指针

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    bool isPalindrome(string s) {
        int i = 0, j = s.size() - 1;
        while (i < j) {
            while (i < j && !isalnum(s[i])) i++;
            while (i < j && !isalnum(s[j])) j--;
            if (isdigit(s[i]) && isdigit(s[j]) && s[i] != s[j]) return false;
            else if (tolower(s[i]) != tolower(s[j])) return false;
            i++;
            j--;
        }

        return true;
    }
};
```

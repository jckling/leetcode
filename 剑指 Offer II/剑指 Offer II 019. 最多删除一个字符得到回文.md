### [剑指 Offer II 019. 最多删除一个字符得到回文](https://leetcode.cn/problems/RQku0D/)

### 双指针

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    bool validPalindrome(string s) {
        int i = 0, j = s.size() - 1;
        for (; i < j && s[i] == s[j]; i++, j--);
        return palindrome(s, i + 1, j) || palindrome(s, i, j - 1);
    }

private:
    bool palindrome(string s, int i, int j) {
        for (; i < j && s[i] == s[j]; i++, j--);
        return i >= j;
    }
};
```

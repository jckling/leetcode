### [剑指 Offer II 002. 二进制加法](https://leetcode.cn/problems/JFETK5/)

### 模拟

- 时间复杂度：O(max(m,n))
- 空间复杂度：O(1)

```c++
class Solution {
public:
    string addBinary(string a, string b) {
        string s;
        int carry = 0;
        int i = a.size() - 1, j = b.size() - 1;
        while (i >= 0 || j >= 0) {
            int x = i >= 0 ? a[i] - '0' : 0;
            int y = j >= 0 ? b[j] - '0' : 0;
            int sum = x + y + carry;
            if (sum % 2) s = '1' + s;
            else s = '0' + s;
            carry = sum / 2;
            i--;
            j--;
        }

        if (carry) s = '1' + s;
        return s;
    }
};
```

### [剑指 Offer 20. 表示数值的字符串](https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof/)

### 模拟

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    bool isNumber(string s) {
        int i = 0;

        // 前导空格
        while (s[i] == ' ') i++;

        // 整数
        bool numeric = scanInteger(s, i);

        // 如果出现'.'，则接下来是数字的小数部分
        if (s[i] == '.') {
            i++;
            // 1.小数可以没有整数部分，如 .123
            // 2.小数点后面可以没有数字，如 233.
            // 3.小数点前后可以都有数字
            numeric = scanUnsignedInteger(s, i) || numeric;
        }

        // 如果出现'e'或者'E'，则接下来是数字的指数部分
        if (s[i] == 'e' || s[i] == 'E') {
            i++;
            // 用 && 的原因：
            // 1.当 e 或 E 前面没有数字时，整个字符串不能表示数字，如 .e1、e1
            // 2.当 e 或 E 后面没有整数时，整个字符串不能表示数字，如 12e，12e+5.4
            numeric = numeric && scanInteger(s, i);
        }

        // 后导空格
        while (s[i] == ' ') i++;

        return numeric && i == s.size();
    }
private:
    bool scanUnsignedInteger(const string &s, int &i) {
        int pos = i;
        while (s[i] != s.size() && s[i] >= '0' && s[i] <= '9') i++;
        // 当 s 中存在若干 0 ~ 9 数字时，返回 true
        return i > pos;
    }
    
    bool scanInteger(const string& s, int &i) {
        // 前导符号
        if (s[i] == '+' || s[i] == '-') i++;
        // 整数
        return scanUnsignedInteger(s, i);
    }
};
```

### [剑指 Offer 67. 把字符串转换成整数](https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/)

### 模拟

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int strToInt(string str) {
        // 长度
        int len = str.size();
        if (len == 0) return 0;
        
        // 前导空格
        int i = 0;
        while (str[i] == ' ') {
            i++;
            if (i == len) return 0;
        }

        // 符号位
        int sign = 1;
        if (str[i] == '-') sign = -1;
        if (str[i] == '-' || str[i] == '+') i++;

        // 求值
        int ans = 0;
        int boundary = INT_MAX / 10;    // 边界
        for (int j = i; j < len; j++) {
            // 非数字
            if (str[j] < '0' || str[j] > '9') break;

            // 1. 执行拼接 10 * res >= 2147483650 越界，即 res 大于 214748364
            // 2. 拼接后是 2147483648 或 2147483649 越界，即最后一位大于 7
            if (ans > boundary || ans == boundary && str[j] > '7') {
                return sign == 1 ? INT_MAX : INT_MIN;
            }

            // 构造
            ans = ans * 10 + (str[j] - '0');
        }

        return sign * ans;
    }
};
```

### [剑指 Offer 46. 把数字翻译成字符串](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

### 动态规划

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int translateNum(int num) {
        string s = to_string(num);
        int a = 1, b = 1, c;    // b 表示长度为 1
        for (int i = 2; i <= s.size(); i++) {
            string t = s.substr(i - 2, 2);
            c = (t.compare("10") >= 0 && t.compare("25") <= 0) ? a + b : b;
            a = b;
            b = c;
        }

        return b;
    }
};
```

优化空间复杂度 O(1)

```c++
class Solution {
public:
    int translateNum(int num) {
        int a = 1, b = 1;           // b 表示最后一位 + 1
        int x, y = num % 10;        // 取最后一位
        while (num > 9) {
            num /= 10;              // 前进一位
            x = num % 10;           // 当前位
            int tmp = x * 10 + y;   // 判断能否看作一个整体
            int c = (tmp >= 10 && tmp <= 25) ? a + b : a;
            b = a;                  // 往前移动
            a = c;
            y = x; 
        }
        return a;
    }
};
```

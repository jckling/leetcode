### [剑指 Offer 44. 数字序列中某一位的数字](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

### 数学

- 时间复杂度：O(logn)
- 空间复杂度：O(logn)

```c++
class Solution {
public:
    int findNthDigit(int n) {
        int digit = 1;  // 记录位数，初始为一位数
        long start = 1; // 记录某一位数的起始数字，1,10,100,...
        long cnt = 9;   // 记录某一位数包含的数字个数，初始一位数个数为 9

        // 确定所求数位所在数字的位数
        while (n > cnt) {
            n -= cnt;
            start *= 10;    // 1,10,100,...
            digit++;        // 1,2,3,...
            cnt = digit * start * 9;    // 9,180,2700,...
        }
        
        // 确定所求数位所在数字
        long num = start + (n - 1) / digit;

        // 确定所求数位在 num 的哪一数位
        return to_string(num)[(n - 1) % digit] - '0';   // 效率
    }
};
```

![](https://pic.leetcode-cn.com/2cd7d8a6a881b697a43f153d6c10e0e991817d78f92b9201b6ab71e44cb619de-Picture1.png)
![](https://pic.leetcode-cn.com/16836ca609f8b4d9af776b35eab4a4c4a86d76f4628a1bc931e56d197617bbb4-Picture2.png)
![](https://pic.leetcode-cn.com/1f2cefd22a9825eb4a52d606a4aee2f93dd659d1b332d3b6a6ed68e5289e8d01-Picture3.png)
![](https://pic.leetcode-cn.com/09af6bd37d9c79d9b904bedef01f0464aee1cd15e18d8a2ea86b70b312a830c3-Picture4.png)

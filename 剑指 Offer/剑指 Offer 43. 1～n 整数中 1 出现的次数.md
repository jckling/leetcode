### [剑指 Offer 43. 1～n 整数中 1 出现的次数](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/)

### 数学

- 时间复杂度：O(logn)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int countDigitOne(int n) {
        // 位因子，初始化为个位
        long digit = 1;

        // 高位、当前位、低位
        int high = n / 10, cur = n % 10, low = 0;
        int res = 0;

        // 当 high 和 cur 同时为 0 时，说明已经越过最高位，因此跳出
        while (high != 0 || cur != 0) {
            // 计算 1 出现次数
            if (cur == 0) res += high * digit;
            else if (cur == 1) res += high * digit + low + 1;
            else res += (high + 1) * digit;

            // 从个位到最高位的递推公式
            low += cur * digit; // 将 cur 加入 low ，组成下轮 low
            cur = high % 10;    // 下轮 cur 是本轮 high 的最低位
            high /= 10;         // 将本轮 high 最低位删除，得到下轮 high
            digit *= 10;        // 位因子每轮 x 10
        }

        return res;
    }
};
```

![](https://pic.leetcode-cn.com/78e60b6c2ada7434ba69643047758e113fa732815f7c53791271c5e0f123687c-Picture1.png)
![](https://pic.leetcode-cn.com/58c7e6472155b49923b48daac10bd438b68e9504690cf45d5e739f3a8cb9cee1-Picture2.png)
![](https://pic.leetcode-cn.com/0e51d37b434ef0ad93882cdcb832f867e18b872833c0c360ad4580eb9ed4aeda-Picture3.png)

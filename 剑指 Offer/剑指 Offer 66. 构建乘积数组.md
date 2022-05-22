### [剑指 Offer 66. 构建乘积数组](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/)

### 数学

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    vector<int> constructArr(vector<int>& a) {
        int len = a.size();
        if (len == 0) return {};

        vector<int> b(len, 1);
        // 从上往下：下三角
        for (int i = 1; i < len; i++) b[i] = b[i - 1] * a[i - 1];

        // 从下往上：上三角
        int tmp = 1;
        for (int i = len - 2; i >= 0; i--) {
            tmp *= a[i + 1];    // 上三角
            b[i] *= tmp;        // 上三角 * 下三角
        }

        return b;
    }
};
```

![](https://pic.leetcode-cn.com/1624619180-vpyyqh-Picture1.png)

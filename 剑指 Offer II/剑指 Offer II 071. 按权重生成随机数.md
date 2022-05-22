### [剑指 Offer II 071. 按权重生成随机数](https://leetcode.cn/problems/cuyjEf/)

### 前缀和 + 二分

- 时间复杂度：初始化 O(n)；选择 O(logn)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<int> sum;    // 前缀和
    Solution(vector<int>& w) {
        sum.resize(w.size() + 1);
        for (int i = 1; i <= w.size(); i++) sum[i] = sum[i - 1] + w[i - 1];
    }
    
    int pickIndex() {
        int n = sum.size();
        int t = (rand() % 100 * 0.01 * sum[n - 1]) + 1;
        int l = 1, r = n - 1;
        while (l < r) {
            int m = (l + r) / 2;
            if (sum[m] >= t) r = m;
            else l = m + 1;
        }
        return r - 1;
    }
};

/**
 * Your Solution object will be instantiated and called as such:
 * Solution* obj = new Solution(w);
 * int param_1 = obj->pickIndex();
 */
```

### [剑指 Offer II 003. 前 n 个数字二进制中 1 的个数](https://leetcode.cn/problems/w3tCBm/)

### 遍历

- 时间复杂度：O(nlogn)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> ans;
        for (int i = 0; i <= n; i++) {
            ans.push_back(count(i));
        }
        return ans;
    }
private:
    int count (int n) {
        int cnt = 0;
        while (n) {
            cnt++;
            n &= (n - 1);
        }
        return cnt;
    }
};
```

### 动态规划

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> ans(n + 1);
        ans[0] = 0;
        for (int i = 1; i <= n; i++) {
            if (i % 2) ans[i] = ans[i - 1] + 1; // 奇数比前面的偶数多一个 1
            else ans[i] = ans[i / 2];           // 偶数比上一个偶数多一个 1
        }
        return ans;
    }
};
```

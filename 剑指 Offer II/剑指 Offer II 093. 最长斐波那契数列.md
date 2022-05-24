### [剑指 Offer II 093. 最长斐波那契数列](https://leetcode.cn/problems/Q91FMA/)

### 动态规划

`dp[i][j]` 表示以 `arr[i], arr[j]` 结尾的子序列的最大长度
- 时间复杂度：O(n^2)
- 空间复杂度：O(n^2)

```c++
class Solution {
public:
    int lenLongestFibSubseq(vector<int>& arr) {
        int n = arr.size();
        unordered_map<int, int> mp;
        for (int i = 0; i < n; i++) mp[arr[i]] = i;

        vector<vector<int>> dp(n, vector<int>(n, 0));
        int ans = 0;
        for (int k = 2; k < n; k++) {
            for (int j = k - 1; j > 0; j--) {
                int diff = arr[k] - arr[j];
                // i, j, k 符合条件
                if (diff < arr[j] && mp.count(diff)) {
                    int i = mp[diff];
                    dp[j][k] = max(dp[j][k], dp[i][j] + 1);
                    ans = max(ans, dp[j][k] + 2);
                }
            }
        }

        return ans >= 3 ? ans : 0;
    }
};
```

将 `arr[i], arr[j]` 视为单个节点 `(i, j)`，求连通路径
- 时间复杂度：O(n^2)
- 空间复杂度：O(nlogm)
    - m 是数组中最大的元素

```c++
class Solution {
public:
    int lenLongestFibSubseq(vector<int>& arr) {
        int n = arr.size();
        unordered_map<int, int> mp; // value->index
        for (int i = 0; i < n; i++) mp[arr[i]] = i;

        unordered_map<int, int> longest;
        int ans = 0;
        for (int k = 0; k < n; k++) {
            for (int j = k - 1; j > 0; j--) {
                int diff = arr[k] - arr[j];
                // 连通 i, j, k
                if (diff < arr[j] && mp.count(diff)) {
                    int i = mp[diff];
                    // dp[j][k] = max(dp[j][k], dp[i][j] + 1);
                    longest[j * n + k] = longest[i * n + j] + 1;
                    ans = max(ans, longest[j * n + k] + 2);
                }
            }
        }

        return ans >= 3 ? ans : 0;
    }
};
```

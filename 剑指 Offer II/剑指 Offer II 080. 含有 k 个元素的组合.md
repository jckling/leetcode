### [剑指 Offer II 080. 含有 k 个元素的组合](https://leetcode.cn/problems/uUsW3B/)

### DFS

- 时间复杂度：$O(C_n^k*k)$
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        dfs(n, k, 1);
        return ans;
    }
private:
    vector<vector<int>> ans;
    vector<int> path;
    void dfs(int n, int k, int idx) {
        if (k == 0) {
            ans.push_back(path);
            return;
        }

        // 剪枝：path 长度加上区间 [cur, n] 的长度小于 k，不可能构造出长度为 k 的 path
        for (int i = idx; i <= n - k + 1; i++) {
            path.push_back(i);
            dfs(n, k - 1, i + 1);
            path.pop_back();
        }
    }
};
```

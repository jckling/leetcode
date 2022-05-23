### [剑指 Offer II 082. 含有重复元素集合的组合](https://leetcode.cn/problems/4sjJUc/)

### DFS

- 时间复杂度：$O(n*2^n)$
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        dfs(candidates, target, 0);
        return ans;
    }
private:
    vector<vector<int>> ans;
    vector<int> tmp;
    void dfs(vector<int>& candidates, int target, int idx) {
        int sum = accumulate(tmp.begin(), tmp.end(), 0);
        if (sum > target) return;
        if (sum == target) {
            ans.push_back(tmp);
            return;
        }

        for (int i = idx; i < candidates.size(); i++) {
            if (i != idx && candidates[i] == candidates[i - 1]) continue;
            tmp.push_back(candidates[i]);
            dfs(candidates, target, i + 1);
            tmp.pop_back();
        }
    }
};
```

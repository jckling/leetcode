### [剑指 Offer II 081. 允许重复选择元素的组合](https://leetcode.cn/problems/Ygoe9J/)

### DFS

- 时间复杂度：$O(n*2^n)$
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
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

        int diff = target - sum;
        for (int i = idx; i < candidates.size(); i++) {
            if (candidates[i] > diff) return;
            tmp.push_back(candidates[i]);
            dfs(candidates, target, i);
            tmp.pop_back();
        }
    }
};
```

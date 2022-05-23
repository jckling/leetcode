### [剑指 Offer II 084. 含有重复元素集合的全排列](https://leetcode.cn/problems/7p8L0Z/)

### DFS

同一层遍历时过滤重复元素

- 时间复杂度：$O(n*n!)$
- 空间复杂度：O(n^2)

```c++
class Solution {
public:
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        vector<bool> st(nums.size(), false);
        sort(nums.begin(), nums.end());
        dfs(nums, st);
        return ans;
    }
private:
    vector<vector<int>> ans;
    vector<int> tmp;
    void dfs(vector<int>& nums, vector<bool>& st) {
        if (tmp.size() == nums.size()) {
            ans.push_back(tmp);
            return;
        }

        for (int i = 0; i < nums.size(); i++) {
            if (st[i]) continue;
            st[i] = true;
            tmp.push_back(nums[i]);
            dfs(nums, st);
            tmp.pop_back();
            st[i] = false;
            while (i + 1 < nums.size() && nums[i + 1] == nums[i]) i++;  // 去重
        }
    }
};
```

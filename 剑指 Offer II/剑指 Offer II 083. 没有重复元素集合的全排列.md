### [剑指 Offer II 083. 没有重复元素集合的全排列](https://leetcode.cn/problems/VvJkup/)

### DFS

- 时间复杂度：$O(n*n!)$
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<bool> st(nums.size(), false);
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
        }
    }
};
```

空间复杂度降低 O(1)

```c++
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        dfs(nums, 0);
        return ans;
    }
private:
    vector<vector<int>> ans;
    void dfs(vector<int>& nums, int idx) {
        if (idx == nums.size()) {
            ans.push_back(nums);
            return;
        }
        for (int i = idx; i < nums.size(); i++) {
            swap(nums[i], nums[idx]);
            dfs(nums, idx + 1);
            swap(nums[i], nums[idx]);
        }
    }
};
```

### [剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

### DFS

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> pathSum(TreeNode* root, int target) {
        dfs(root, target);
        return ans;
    }
private:
    vector<vector<int>> ans;
    vector<int> path;
    void dfs(TreeNode* root, int target) {
        if (!root) return;
        
        target -= root->val;
        path.emplace_back(root->val);

        if (!root->left && !root->right && target == 0) ans.emplace_back(path);
        if (root->left) dfs(root->left, target);
        if (root->right) dfs(root->right, target);

        path.pop_back();
    }
};
```

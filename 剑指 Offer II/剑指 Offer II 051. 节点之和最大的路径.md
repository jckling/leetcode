### [剑指 Offer II 051. 节点之和最大的路径](https://leetcode.cn/problems/jC7MId/)

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
    int maxPathSum(TreeNode* root) {
        dfs(root);
        return ans;
    }
private:
    int ans = INT_MIN;
    int dfs (TreeNode* root) {
        if (!root) return 0;

        int left = dfs(root->left);    // 左子树
        int right = dfs(root->right);  // 右子树

        // 当前子树内部的最大路径和
        int inner = root->val + left + right;

        // 全局的最大路径和
        ans = max(ans, inner);

        // 当前子树对外提供的最大路径和，不能两头收益
        int outer = root->val + max(0, max(left, right)); 

        // 如果对外提供的最大路径和为负，直接返回 0
        return max(0, outer);
    }
};
```

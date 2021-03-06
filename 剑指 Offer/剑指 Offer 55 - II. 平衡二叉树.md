### [剑指 Offer 55 - II. 平衡二叉树](https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/)

### 递归

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        return dfs(root) != -1;
    }
private:
    int dfs(TreeNode* root) {
        if (!root) return 0;

        int l = dfs(root->left);
        if (l == -1) return -1;

        int r = dfs(root->right);
        if (r == -1) return -1;

        // 深度差大于 1，返回 -1
        return abs(l - r) <= 1 ? max(l, r) + 1 : -1;
    }
};
```

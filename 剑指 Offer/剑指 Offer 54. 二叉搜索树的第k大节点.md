### [剑指 Offer 54. 二叉搜索树的第 k 大节点](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

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
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int kthLargest(TreeNode* root, int k) {
        kth = k;
        dfs(root);  // 右根左
        return val;
    }
private:
    int kth, val;
    void dfs(TreeNode* root) {
        if (!root) return;

        dfs(root->right);

        if (kth == 0) return;
        if (--kth == 0) val = root->val;

        dfs(root->left);
    }
};
```

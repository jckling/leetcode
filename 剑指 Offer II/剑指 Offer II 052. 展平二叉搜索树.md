### [剑指 Offer II 052. 展平二叉搜索树](https://leetcode.cn/problems/NYBBNL/)

### DFS

中序遍历的同时修改指向，使用 `pre` 保存上一节点

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
    TreeNode* increasingBST(TreeNode* root) {
        TreeNode* dummy = new TreeNode();
        pre = dummy;
        dfs(root);
        return dummy->right;
    }
private:
    TreeNode* pre;
    void dfs(TreeNode* root) {
        if (!root) return;
        dfs(root->left);
        pre->right = root;
        root->left = nullptr;
        pre = root;
        dfs(root->right);
    }
};
```

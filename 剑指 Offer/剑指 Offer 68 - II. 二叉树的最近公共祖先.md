### [剑指 Offer 68 - II. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

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
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        // 越过叶节点，或等于 p、q
        if (!root || root == p || root == q) return root;

        // 查找 p、q
        TreeNode* l = lowestCommonAncestor(root->left, p, q);
        TreeNode* r = lowestCommonAncestor(root->right, p, q);

        if (!l && !r) return nullptr;   // 左右子树都不包含 p、q
        if (l == nullptr) return r;     // 在右子树
        if (r == nullptr) return l;     // 在左子树
        return root;                    // p、q 分别在左右子树
    }
};
```

### [剑指 Offer 28. 对称的二叉树](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)

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
    bool isSymmetric(TreeNode* root) {
        if (!root) return true;
        return recur(root->left, root->right);
    }
private:
    bool recur(TreeNode* A, TreeNode* B) {
        if (!A && !B) return true;
        if (!A || !B || A->val != B->val) return false;
        return recur(A->left, B->right) && recur(A->right, B->left);
    }
};
```

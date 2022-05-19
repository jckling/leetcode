### [剑指 Offer II 053. 二叉搜索树中的中序后继](https://leetcode.cn/problems/P5rCT8/)

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
    TreeNode* ans;
    TreeNode* pre;
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
        if (!root) return nullptr;
        inorderSuccessor(root->left, p);
        if (pre && pre->val == p->val) ans = root;
        pre = root;
        inorderSuccessor(root->right, p);
        return ans;
    }
};
```

利用二叉搜索树性质：左 < 根 < 右

- 时间复杂度：O(n)
- 空间复杂度：O(1)

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
    TreeNode* ans;
    
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
        if (!root) return nullptr;
        TreeNode* succ = nullptr;
        // 在右子树
        if (p->right) {
            succ = p->right;
            while (succ->left) succ = succ->left;
            return succ;
        }
        // 无右子树，从根查找
        while (root) {
            // 左 < 根 < 右
            if (root->val > p->val) {
                succ = root;
                root = root->left;
            }
            else root = root->right;
        }
        return succ;
    }
};
```

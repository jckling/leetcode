### [剑指 Offer 68 - I. 二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

### 遍历

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
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        while (root) {
            if (root->val < p->val && root->val < q->val) root = root->right;       // 都比 root 小
            else if (root->val > p->val && root->val > q->val) root = root->left;   // 都比 root 大
            else break;
        }
        return root;
    }
};
```

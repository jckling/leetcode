### [剑指 Offer II 043. 往完全二叉树添加节点](https://leetcode.cn/problems/NaqhDT/)

### BFS

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
class CBTInserter {
public:
    CBTInserter(TreeNode* _root) : root(_root) {
        q.push(root);
        while (q.front()->left && q.front()->right) {
            q.push(q.front()->left);
            q.push(q.front()->right);
            q.pop();    // 弹出有左右子树的节点
        }
    }
    
    int insert(int v) {
        TreeNode* parent = q.front();       // 父节点
        TreeNode* node = new TreeNode(v);   // 新节点

        // 优先插入左子树
        if (!parent->left) parent->left = node;
        else {  // 然后再考虑右子树
            parent->right = node;
            // 作为下一层的父节点
            q.push(parent->left);
            q.push(parent->right);
            q.pop();    // 弹出有左右子树的节点
        }
        return parent->val;
    }
    
    TreeNode* get_root() {
        return root;
    }
private:
    TreeNode* root;
    queue<TreeNode*> q;
};

/**
 * Your CBTInserter object will be instantiated and called as such:
 * CBTInserter* obj = new CBTInserter(root);
 * int param_1 = obj->insert(v);
 * TreeNode* param_2 = obj->get_root();
 */
```

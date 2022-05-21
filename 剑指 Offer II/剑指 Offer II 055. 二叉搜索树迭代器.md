### [剑指 Offer II 055. 二叉搜索树迭代器](https://leetcode.cn/problems/kTOapQ/)

### DFS

中序遍历，存储到队列中

- 时间复杂度：构造队列 O(n)；返回元素 O(1)
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
class BSTIterator {
public:
    BSTIterator(TreeNode* _root) : root(_root) {
        dfs(root);
    }
    
    int next() {
        int val = q.front();
        q.pop();
        return val;
    }
    
    bool hasNext() {
        return !q.empty();
    }
private:
    TreeNode* root;
    queue<int> q;
    void dfs(TreeNode* root) {
        if (!root) return;
        dfs(root->left);
        q.push(root->val);
        dfs(root->right);
    }
};

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator* obj = new BSTIterator(root);
 * int param_1 = obj->next();
 * bool param_2 = obj->hasNext();
 */
```

### 单调栈

- 时间复杂度：O(1)
- 空间复杂度：O(h)

```c++
class BSTIterator {
public:
    stack<TreeNode*> stk;   // 保存左节点
    BSTIterator(TreeNode* root) {
        while (root) {
            stk.push(root);
            root = root->left;
        }
    }
    
    int next() {
        TreeNode* node = stk.top();
        stk.pop();
        int val = node->val;
        node = node->right;
        while (node) {
            stk.push(node);
            node = node->left;
        }
        return val;
    }
    
    bool hasNext() {
        return !stk.empty();
    }
};
```

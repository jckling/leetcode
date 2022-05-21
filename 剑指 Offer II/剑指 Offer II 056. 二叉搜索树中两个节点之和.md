### [剑指 Offer II 056. 二叉搜索树中两个节点之和](https://leetcode.cn/problems/opLdQZ/)

### 递归

集合存储值（值唯一）

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
    unordered_set<int> st;
    bool findTarget(TreeNode* root, int k) {
        if (!root) return false;
        if (st.find(k - root->val) != st.end()) return true;
        st.insert(root->val);
        return findTarget(root->left, k) || findTarget(root->right, k);
    }
};
```

### 双指针

利用二叉搜索树性质：左 < 根 < 右

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
    bool findTarget(TreeNode* root, int k) {
        if (!root) return false;
        stack<TreeNode*> lstk, rstk;

        // 左节点
        TreeNode* curr = root;
        while (curr) {
            lstk.push(curr);
            curr = curr->left;
        }

        // 右节点
        curr = root;
        while (curr) {
            rstk.push(curr);
            curr = curr->right;
        }

        // 比值
        TreeNode* l = lstk.top();   // 最小值
        TreeNode* r = rstk.top();   // 最大值
        while (l->val < r->val) {
            int sum = l->val + r->val;
            if (sum < k) l = getNext(lstk, true);
            else if (sum > k) r = getNext(rstk, false);
            else return true;
        }

        return false;
    }
private:
    TreeNode* getNext(stack<TreeNode*>& stk, bool isLeft) {
        TreeNode* node = stk.top();
        stk.pop();
        TreeNode* succ = isLeft ? node->right : node->left;
        while (succ) {
            stk.push(succ);
            succ = isLeft ? succ->left : succ->right;
        }
        return stk.top();
    }
};
```

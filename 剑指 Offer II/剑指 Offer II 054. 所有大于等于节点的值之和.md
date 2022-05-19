### [剑指 Offer II 054. 所有大于等于节点的值之和](https://leetcode.cn/problems/w6cpku/)

### 递归

反序中序遍历：右根左

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
    int sum = 0;
    TreeNode* convertBST(TreeNode* root) {
        if (!root) return nullptr;
        convertBST(root->right);    // 右
        sum += root->val;           // 根
        root->val = sum;            // 累加
        convertBST(root->left);     // 左
        return root;
    }
};
```

### Morris 遍历

使用指针将树当作链表遍历

- 时间复杂度：O(n)
- 空间复杂度：O(1)

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
    TreeNode* convertBST(TreeNode* root) {
        int sum = 0;
        TreeNode* node = root;

        while (node) {
            if (!node->right) {             // 右节点为空
                sum += node->val;           // 处理当前节点
                node->val = sum;
                node = node->left;          // 遍历左节点
            }
            else {
                TreeNode* succ = getSuccessor(node);
                if (!succ->left) {          // 左节点为空
                    succ->left = node;
                    node = node->right;     // 遍历右节点
                }
                else {
                    succ->left = nullptr;
                    sum += node->val;       // 处理当前节点
                    node->val = sum;
                    node = node->left;
                }
            }
        }

        return root;
    }
private:
    TreeNode* getSuccessor(TreeNode* node) {
        TreeNode* succ = node->right;
        while (succ->left && succ->left != node) succ = succ->left;
        return succ;
    }
};
```

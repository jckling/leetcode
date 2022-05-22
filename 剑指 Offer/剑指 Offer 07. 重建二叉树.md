### [剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

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
    // 前序：左根右
    // 中序：根左右
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        // root = inorder[0]
        // preorder = left root right

        // 暂存
        this->preorder = preorder;
        // 初始化中序遍历索引（没有重复数字）
        for(int i = 0; i < inorder.size(); i++) dic[inorder[i]] = i;

        // 按照「根左右」的顺序构建
        return recur(0, 0, inorder.size() - 1);
    }
private:
    vector<int> preorder;
    unordered_map<int, int> dic;
    TreeNode* recur(int root, int left, int right) {
        if(left > right) return nullptr;
        TreeNode* node = new TreeNode(preorder[root]);  // 根

        // 划分点
        int i = dic[preorder[root]];
        node->left = recur(root + 1, left, i - 1);  // 左
        node->right = recur(root + i - left + 1, i + 1, right); // 右
        
        return node;
    }
};
```

### [剑指 Offer 32 - III. 从上到下打印二叉树 III](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

### BFS

双端队列

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> ans;
        if (!root) return ans;

        deque<TreeNode*> q;
        q.push_back(root);
        while (!q.empty()) {
            int n = q.size();
            vector<int> odd;
            while (n--) {   // 从左往右
                TreeNode* node = q.front(); // 前
                q.pop_front();
                odd.emplace_back(node->val);
                if (node->left) q.push_back(node->left);    // 左
                if (node->right) q.push_back(node->right);  // 右
            }

            ans.emplace_back(odd);
            if (q.empty()) break;

            vector<int> even;
            n = q.size();
            while (n--) {   // 从右往左
                TreeNode* node = q.back();  // 后
                q.pop_back();
                even.emplace_back(node->val);
                if (node->right) q.push_front(node->right); // 右
                if (node->left) q.push_front(node->left);   // 左
            }

            ans.emplace_back(even);
        }

        return ans;
    }
};
```

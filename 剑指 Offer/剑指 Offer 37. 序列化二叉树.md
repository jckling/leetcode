### [剑指 Offer 37. 序列化二叉树](https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/)

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
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        if (!root) return "";

        string s;
        queue<TreeNode*> q;
        q.push(root);
        while (!q.empty()) {
            TreeNode* node = q.front();
            q.pop();
            if (!node) s += "null,";
            else {
                s += to_string(node->val) + ",";
                q.push(node->left);
                q.push(node->right);
            }
        }

        return s;
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        if (data.size() == 0) return nullptr;
        vector<TreeNode*> v;

        istringstream iss(data);
        string s;
        while (getline(iss, s, ',')) {
            if (s != "null") v.emplace_back(new TreeNode(stoi(s)));
            else v.emplace_back(nullptr);
        }

        int idx = 1;
        for (int i = 0; i < v.size(); i++) {
            if (!v[i]) continue;
            v[i]->left = v[idx++];
            v[i]->right = v[idx++];
        }
        return v[0];
    }
};

// Your Codec object will be instantiated and called as such:
// Codec codec;
// codec.deserialize(codec.serialize(root));
```

### [剑指 Offer 36. 二叉搜索树与双向链表](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

### DFS

二叉搜索树的中序遍历为递增序列

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;

    Node() {}

    Node(int _val) {
        val = _val;
        left = NULL;
        right = NULL;
    }

    Node(int _val, Node* _left, Node* _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/
class Solution {
public:
    Node* treeToDoublyList(Node* root) {
        if (!root) return root;
        dfs(root);
        head->left = prev;  // 头
        prev->right = head; // 尾
        return head;
    }
private:
    Node* prev, * head;
    void dfs (Node* root) {
        if (!root) return;

        // 中序遍历
        dfs(root->left);
        if (!prev) head = root; // 没有前驱（最左下）的节点为链表头
        else {
            prev->right = root; // 前驱节点的右指针指向当前节点
            root->left = prev;  // 当前节点的左指针指向前驱节点
        }
        prev = root;            // 记录前驱节点
        dfs(root->right);
    }
};
```

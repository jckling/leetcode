### [剑指 Offer II 029. 排序的循环链表](https://leetcode.cn/problems/4ueAj6/)

### 遍历

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;

    Node() {}

    Node(int _val) {
        val = _val;
        next = NULL;
    }

    Node(int _val, Node* _next) {
        val = _val;
        next = _next;
    }
};
*/

class Solution {
public:
    Node* insert(Node* head, int insertVal) {
        if (!head) {
            Node* node = new Node(insertVal);
            node->next = node;
            return node;
        }

        Node* curr = head;
        while (curr->next != head) {
            // 边界
            if (curr->next->val < curr->val) {
                if (curr->val <= insertVal) break;          // 比最大值大
                if (insertVal <= curr->next->val) break;    // 比最小值小
            }
            if (curr->val <= insertVal && insertVal <= curr->next->val) break;
            curr = curr->next;
        }

        curr->next = new Node(insertVal, curr->next);
        return head;
    }
};
```

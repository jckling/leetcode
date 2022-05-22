### [剑指 Offer 35. 复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

### 哈希表

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/
class Solution {
public:
    Node* copyRandomList(Node* head) {
        unordered_map<Node*, Node*> mp;
        Node* curr = head;
        while (curr) {
            mp[curr] = new Node(curr->val);
            curr = curr->next;
        }

        curr = head;
        while (curr) {
            mp[curr]->next = mp[curr->next];
            mp[curr]->random = mp[curr->random];
            curr = curr->next;
        }

        return mp[head];
    }
};
```

### 拼接 + 拆分

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    Node* copyRandomList(Node* head) {
        // 特殊情况
        if (!head) return head;

        // 复制节点，构建拼接链表
        Node* curr = head;
        while (curr) {
            Node* node = new Node(curr->val);
            node->next = curr->next;
            curr->next = node;
            curr = node->next;
        }

        // 更新 random
        curr = head;
        while (curr) {
            if (curr->random) curr->next->random = curr->random->next;
            curr = curr->next->next;
        }

        Node* res = head->next; // 新链表头指针
        curr = res;             // 新链表
        Node* prev = head;      // 原链表
        while (curr->next) {
            prev->next = prev->next->next;
            curr->next = curr->next->next;
            prev = prev->next;
            curr = curr->next;
        }

        // 处理原链表尾节点
        prev->next = nullptr;

        return res;
    }
};
```

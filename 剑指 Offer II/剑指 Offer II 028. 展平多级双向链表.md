### [剑指 Offer II 028. 展剑指 Offer II 028. 展平多级双向链表平多级双向链表](https://leetcode.cn/problems/Qv1Da2/)

### 迭代

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* prev;
    Node* next;
    Node* child;
};
*/

class Solution {
public:
    Node* flatten(Node* head) {
        Node* dummy = new Node(0);
        dummy->next = head;
        for (; head; head = head->next) {
            if (head->child) {
                Node* node = head->next;        // 后继
                Node* child = head->child;      // 子链表
                head->next = child;             // 指向下一层
                child->prev = head;             // 指向本层
                head->child = nullptr;          // 清除 child 指针
                Node* last = head;              // 下一层最后一个节点
                while (last->next) last = last->next;
                last->next = node;              // 链接本层结束
                if (node) node->prev = last;
            }
        }

        return dummy->next;
    }
};
```

### 递归

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    Node* flatten(Node* head) {
        dfs(head);
        return head;
    }
private:
    Node* dfs(Node* head) {
        Node* last = head;
        while (head) {
            if (head->child == nullptr) {   // 没有子链表，往前走
                last = head;
                head = head->next;
            }
            else {
                Node* node = head->next;            // 后继
                Node* childLast = dfs(head->child); // 下一层的结束位置
                head->next = head->child;           // 指向下一层
                head->child->prev = head;           // 指向上一层
                head->child = nullptr;              // 清除 child 指针
                if (childLast) childLast->next = node;  // 下一层结束链接上一层后继
                if (node) node->prev = childLast;       // 指向下一层结束
                last = head;
                head = childLast;
            }
        }

        return last;
    }
};
```

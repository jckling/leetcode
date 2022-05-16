### [剑指 Offer II 024. 反转链表](https://leetcode.cn/problems/UHnkqh/)

### 遍历

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */

class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* pre = nullptr;
        while (head) {
            ListNode* node = head->next;
            head->next = pre;
            pre = head;
            head = node;
        }
        return pre;
    }
};
```

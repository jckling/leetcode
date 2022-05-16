### [剑指 Offer II 021. 删除链表的倒数第 n 个结点](https://leetcode.cn/problems/SLwz0R/)

### 双指针

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* l = head, * r = head;
        while (n--) {
            if (r) r = r->next;
            else return head;
        }
        if (r == nullptr) return head->next;

        while (r->next) {
            l = l->next;
            r = r->next;
        }

        l->next = l->next->next;
        return head;
    }
};
```

### [剑指 Offer II 022. 链表中环的入口节点](https://leetcode.cn/problems/c32eOV/)

### 双指针

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* slow = head;
        ListNode* fast = head;

        // 第一次相遇
        while (true) {
            if (!fast || !fast->next) return nullptr;
            fast = fast->next->next;
            slow = slow->next;
            if (fast == slow) break;
        }

        // 第二次相遇
        fast = head;
        while (slow != fast) {
            slow = slow->next;
            fast = fast->next;
        }
        return fast;
    }
};
```

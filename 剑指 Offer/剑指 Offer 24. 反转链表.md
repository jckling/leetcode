### [剑指 Offer 24. 反转链表](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/)

### 双指针

时间复杂度：O(n)
空间复杂度：O(1)

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* pre = nullptr, * cur = head;
        while (cur) {
            ListNode* node = cur->next;
            cur->next = pre;
            pre = cur;
            cur = node;
        }

        return pre;
    }
};
```

### [剑指 Offer II 023. 两个链表的第一个重合节点](https://leetcode.cn/problems/3u1WK4/)

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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* A = headA;
        ListNode* B = headB;

        while (A != B) {
            A = A ? A->next : headB;
            B = B ? B->next : headA;
        }

        return A;
    }
};
```

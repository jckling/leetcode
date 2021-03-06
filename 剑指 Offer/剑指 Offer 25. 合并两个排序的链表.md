### [剑指 Offer 25. 合并两个排序的链表](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

### 遍历

- 时间复杂度：O(m+n)
- 空间复杂度：O(1)

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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* dummy = new ListNode();
        ListNode* head = dummy;

        while (l1 && l2) {
            if (l1->val < l2->val) {
                head->next = new ListNode(l1->val);
                l1 = l1->next;
            }
            else {
                head->next = new ListNode(l2->val);
                l2 = l2->next;
            }
            head = head->next;
        }

        head->next = l1 ? l1 : l2;

        return dummy->next;

    }
};
```

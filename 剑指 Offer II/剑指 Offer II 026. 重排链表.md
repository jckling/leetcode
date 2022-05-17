### [剑指 Offer II 026. 重排链表](https://leetcode.cn/problems/LGjMqU/)

### 中点 + 反转 + 合并

目标链表是将原链表的左半端和反转后的右半端合并后的结果。

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
    void reorderList(ListNode* head) {
        if (!head) return;

        ListNode* mid = middleNode(head);   // 中点
        ListNode* l1 = head;                // 左链表
        ListNode* l2 = mid->next;           // 右链表
        mid->next = nullptr;                // 断开

        l2 = reverseList(l2);               // 翻转右链表
        mergeList(l1, l2);                  // 交错拼接
    }

private:
    // 快慢指针找中点
    ListNode* middleNode(ListNode* head) {
        ListNode* slow = head;
        ListNode* fast = head;
        while (fast->next && fast->next->next) {
            slow = slow->next;
            fast = fast->next->next;
        }

        return slow;
    }
  
    // 翻转链表
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = nullptr;
        while (head) {
            ListNode* node = head->next;
            head->next = prev;
            prev = head;
            head = node;
        }

        return prev;
    }

    // 合并链表（l1 l2 l1 l2）
    void mergeList(ListNode* l1, ListNode* l2) {
        ListNode* t1;
        ListNode* t2;
        while (l1 && l2) {
            t1 = l1->next;
            l1->next = l2;
            l1 = t1;

            t2 = l2->next;
            l2->next = l1;
            l2 = t2;
        }
    }
};
```

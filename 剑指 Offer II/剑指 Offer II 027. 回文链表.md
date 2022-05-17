### [剑指 Offer II 027. 回文链表](https://leetcode.cn/problems/aMhZSa/)

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
    bool isPalindrome(ListNode* head) {
        ListNode* fast = head;
        ListNode* slow = head;

        // 中点
        while (fast) {
            fast = fast->next;
            if (fast) fast = fast->next;
            slow = slow->next;
        }

        // 翻转
        ListNode* pre = reverseList(slow);

        // 判断
        while (head && pre) {
            if (head->val != pre->val) return false;
            head = head->next;
            pre = pre->next;
        }

        return true;
    }

private:
    // 反转链表
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = nullptr;
        while (head) {
            ListNode* next = head->next;
            head->next = prev;
            prev = head;
            head = next;
        }

        return prev;
    }
};
```

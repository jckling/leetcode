### [剑指 Offer II 025. 链表中的两数相加](https://leetcode.cn/problems/lMSNwu/)

### 栈

- 时间复杂度：O(max(m, n))
- 空间复杂度：O(m+n)

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        stack<int> stk1;
        while (l1) {
            stk1.push(l1->val);
            l1 = l1->next;
        }

        stack<int> stk2;
        while (l2) {
            stk2.push(l2->val);
            l2 = l2->next;
        }

        ListNode* pre = nullptr;
        int carry = 0;
        while (!stk1.empty() || !stk2.empty() || carry) {
            int a = stk1.empty() ? 0 : stk1.top();
            int b = stk2.empty() ? 0 : stk2.top();
            if (!stk1.empty()) stk1.pop();
            if (!stk2.empty()) stk2.pop();

            int sum = a + b + carry;
            carry = sum / 10;
            ListNode* node = new ListNode(sum % 10);

            node->next = pre;
            pre = node;
        }

        return pre;
    }
};
```

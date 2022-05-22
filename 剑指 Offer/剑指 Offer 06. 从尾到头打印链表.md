### [剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

### 遍历

遍历两遍

- 时间复杂度：O(n)
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
    vector<int> reversePrint(ListNode* head) {
        ListNode* cur = head;
        int cnt = 0;
        while(cur) {
            cur = cur->next;
            cnt++;
        }

        vector<int> ans(cnt);
        cnt--;
        while(head && cnt >= 0) {
            ans[cnt--] = head->val;
            head = head->next;
        }
        return ans;
    }
};
```

## 栈

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        stack<int> stk;
        while (head) {
            stk.push(head->val);
            head = head->next;
        }
        
        vector<int> ans;
        while(!stk.empty()) {
            ans.emplace_back(stk.top());
            stk.pop();
        }
        return ans;
    }
};
```

## 递归

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        recur(head);
        return res;
    }
private:
    vector<int> res;
    void recur(ListNode* head){
        if(!head) return;
        recur(head->next);
        res.push_back(head->val);
    }
};
```

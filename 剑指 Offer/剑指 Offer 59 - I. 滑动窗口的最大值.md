### [剑指 Offer 59 - I. 滑动窗口的最大值](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

### 单调栈

- 时间复杂度：O(n)
- 空间复杂度：O(k)

```c++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        if (k == 1 || nums.size() <= 1) return nums;

        // 初始化窗口
        deque<int> q;
        for (int i = 0; i < k; i++) {
            while (!q.empty() && q.back() < nums[i]) q.pop_back();
            q.push_back(nums[i]);
        }

        vector<int> ans;
        ans.push_back(q.front());
        for (int i = k; i < nums.size(); i++) {
            // 移出窗口
            if (q.front() == nums[i - k]) q.pop_front();
            // 保持递减
            while (!q.empty() && q.back() < nums[i]) q.pop_back();
            q.push_back(nums[i]);
            ans.push_back(q.front());
        }

        return ans;
    }
};
```

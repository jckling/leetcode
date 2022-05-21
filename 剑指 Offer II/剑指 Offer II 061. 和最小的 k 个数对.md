### [剑指 Offer II 061. 和最小的 k 个数对](https://leetcode.cn/problems/qn8gGX/)

### 小根堆

优先队列

- 时间复杂度：O(klogk)
- 空间复杂度：O(k)

```c++
class Solution {
public:
    vector<vector<int>> kSmallestPairs(vector<int>& nums1, vector<int>& nums2, int k) {
        auto cmp = [&nums1, &nums2](const pair<int, int> & a, const pair<int, int> & b) {
            return nums1[a.first] + nums2[a.second] > nums1[b.first] + nums2[b.second];
        };
        priority_queue<pair<int, int>, vector<pair<int, int>>, decltype(cmp)> q(cmp);

        // k 个元素入堆（nums1 的下标）
        int m = nums1.size(), n = nums2.size();
        for (int i = 0; i < min(m, k); i++) q.emplace(i, 0);
        
        vector<vector<int>> ans;
        while (k-- > 0 && !q.empty()) {
            auto [i, j] = q.top(); 
            q.pop();
            ans.push_back({nums1[i], nums2[j]});
            if (j + 1 < n) { // 添加一对
                q.emplace(i, j + 1);
            }
        }
        return ans;
    }
};
```

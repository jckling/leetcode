### [剑指 Offer II 060. 出现频率最高的 k 个数字](https://leetcode.cn/problems/g5c51o/)

### 小根堆

优先队列，哈希表统计频率

- 时间复杂度：O(nlogk)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> mp;
        for (auto& num : nums) mp[num]++;

        priority_queue<pair<int, int>, vector<pair<int, int>>, cmp> q;
        for (auto& p : mp) {
            q.push(p);
            if (q.size() > k) q.pop();
        }

        vector<int> ans;
        while (!q.empty()) {
            ans.emplace_back(q.top().first);
            q.pop();
        }

        return ans;
    }
private:
    struct cmp {
        bool operator() (pair<int, int>& a, pair<int, int>& b) {
            return a.second > b.second;   // 小根堆使用大于号
        }
    };
};
```

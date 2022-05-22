### [剑指 Offer II 074. 合并区间](https://leetcode.cn/problems/SsGoHC/)

### 排序

- 时间复杂度：O(nlogn)
- 空间复杂度：O(logn)

```c++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end());

        vector<vector<int>> ans;
        int st = intervals[0][0], ed = intervals[0][1];
        for (int i = 1; i < intervals.size(); i++) {
            int l = intervals[i][0], r = intervals[i][1];
            if (ed < l) {
                ans.push_back({st, ed});
                st = l;
                ed = r;
            }
            else ed = max(ed ,r);
        }

        ans.push_back({st, ed});
        return ans;
    }
};
```

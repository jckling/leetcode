### [剑指 Offer 57 - II. 和为 s 的连续正数序列](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

### 双指针

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    vector<vector<int>> findContinuousSequence(int target) {
        vector<vector<int>> ans;
        int i = 1, j = 2;
        int sum = 3;
        while (i < j) {
            if (sum < target) {
                j++;
                sum += j;
            }
            else {
                if (sum == target) {
                    vector<int> tmp(j - i + 1);
                    iota(tmp.begin(), tmp.end(), i);
                    ans.push_back(tmp);
                }
                sum -= i;
                i++;
            }
        }

        return ans;
    }
};
```

### [剑指 Offer II 069. 山峰数组的顶部](https://leetcode.cn/problems/B1IidL/)

### 二分

- 时间复杂度：O(logn)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int peakIndexInMountainArray(vector<int>& arr) {
        int l = 0, r = arr.size() - 1;
        while (l < r) {
            int m = (l + r) / 2;
            if (arr[m - 1] < arr[m] && arr[m] > arr[m + 1]) return m;
            if (arr[m] < arr[m + 1]) l = m;         // 最值在右侧
            else if (arr[m] > arr[m + 1]) r = m;    // 最值在左侧
        }
        return l;
    }
};
```

### [剑指 Offer 40. 最小的 k 个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

### 快排

- 时间复杂度：O(n)
- 空间复杂度：O(logn)

```c++
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        if (k >= arr.size()) return arr;
        return qsort(arr, 0, arr.size() - 1, k);
    }
private:
    vector<int> qsort(vector<int>& a, int l, int r, int k) {
        int i = l, j = r;
        while (i < j) {
            while (i < j && a[j] >= a[l]) j--;  // 注意顺序
            while (i < j && a[i] <= a[l]) i++;
            swap(a[i], a[j]);
        }
        swap(a[l], a[i]);

        if (i > k) return qsort(a, l, i - 1, k);
        if (i < k) return qsort(a, i + 1, r, k);
        return vector<int>{a.begin(), a.begin() + k};
    }
};
```

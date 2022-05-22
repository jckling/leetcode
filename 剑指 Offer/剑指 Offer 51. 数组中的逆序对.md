### [剑指 Offer 51. 数组中的逆序对](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)

### 归并排序

- 时间复杂度：O(nlogn)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int reversePairs(vector<int>& nums) {
        vector<int> tmp(nums.size());
        return mergeSort(nums, 0, nums.size() - 1, tmp);
    }
private:
    int mergeSort(vector<int>& nums, int l, int r, vector<int>& tmp) {
        if (l >= r) return 0;

        // 递归划分
        int m = (l + r) / 2;
        int res = mergeSort(nums, l, m, tmp) + mergeSort(nums, m + 1, r, tmp);

        // 暂存
        for (int k = l; k <= r; k++) tmp[k] = nums[k];
        
        // 合并
        int i = l, j = m + 1;   // 左右区间起始索引
        for (int k = l; k <= r; k++) {
            // 左子数组合并完毕
            if (i == m + 1) nums[k] = tmp[j++];

            // 右子数组合并完毕、左子数组元素小于右子数组元素
            else if (j == r + 1 || tmp[i] <= tmp[j]) nums[k] = tmp[i++];

            // 左子数组元素大于右子数组元素
            else {
                nums[k] = tmp[j++];
                res += m - i + 1;   // 统计逆序对
            }
        }

        return res;
    }
};
```

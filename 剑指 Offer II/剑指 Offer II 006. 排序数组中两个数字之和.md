### [剑指 Offer II 006. 排序数组中两个数字之和](https://leetcode.cn/problems/kLl5u1/)

### 双指针

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int i = 0, j = numbers.size() - 1;
        while (i < j) {
            if (numbers[i] + numbers[j] > target) j--;
            else if (numbers[i] + numbers[j] < target) i++;
            else return {i, j};
        }
        return {};
    }
};
```

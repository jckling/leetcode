### [剑指 Offer 39. 数组中出现次数超过一半的数字](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

### 数学

摩尔计数

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int x = nums[0];
        int votes = 0;
        for (auto& num : nums) {
            if (votes == 0) x = num;
            votes += num == x ? 1 : -1;
        }
        return x;
    }
};
```

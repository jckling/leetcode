### [剑指 Offer 61. 扑克牌中的顺子](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

### 排序

- 时间复杂度：O(1)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    bool isStraight(vector<int>& nums) {
        sort(nums.begin(), nums.end());

        int joker = 0;
        for (int i = 0; i < 4; i++) {
            if (nums[i] == 0) joker++; // 统计大小王数量
            else if (nums[i] == nums[i + 1]) return false; // 重复，提前返回
        }

        return nums[4] - nums[joker] < 5;
    }
};
```

## 哈希表

- 时间复杂度：O(1)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    bool isStraight(vector<int>& nums) {
        unordered_set<int> repeat;
        int ma = 0, mi = 14;
        for (auto& num : nums) {
            if (num == 0) continue;  // 跳过大小王
            ma = max(ma, num);
            mi = min(mi, num);
            if (repeat.find(num) != repeat.end()) return false;  // 重复，提前返回
            repeat.insert(num);
        }
        return ma - mi < 5;
    }
};
```

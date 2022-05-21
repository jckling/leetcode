### [剑指 Offer II 057. 值和下标之差都在给定的范围内](https://leetcode.cn/problems/7WqeDu/)

### 红黑树

查询和增删频率相当时，使用红黑树，维护滑动窗口

- 时间复杂度：O(nlogk)
- 空间复杂度：O(k)

```c++
class Solution {
public:
    bool containsNearbyAlmostDuplicate(vector<int>& nums, int k, int t) {
        set<long> st;   // 滑动窗口
        for (int i = 0; i < nums.size(); i++) {
            auto lb = st.lower_bound((long) nums[i] - t);   // 下界
            if (lb != st.end() && *lb <= (long) nums[i] + t) return true;
            st.insert(nums[i]);
            if (i >= k) st.erase(nums[i - k]);
        }
        return false;
    }
};
```

### 桶排序

- 时间复杂度：O(n)
- 空间复杂度：O(k)

```c++
typedef long long LL;
class Solution {
public:
    bool containsNearbyAlmostDuplicate(vector<int>& nums, int k, int t) {
        size = t + 1L;
        int n = nums.size();
        unordered_map<int, int> mp;
        for (int i = 0; i < n; i++) {
            LL u = nums[i];
            int idx = getIdx(u); 
            // 目标桶已存在（桶不为空），说明前面已有 [u - t, u + t] 范围的数字
            if (mp.find(idx) != mp.end()) return true;
            // 检查相邻的桶
            int l = idx - 1, r = idx + 1;
            if (mp.find(l) != mp.end() && abs(u - mp[l]) <= t) return true;
            if (mp.find(r) != mp.end() && abs(u - mp[r]) <= t) return true;
            // 建立目标桶
            mp[idx] = u;
            // 移除下标范围不在 [max(0, i - k), i) 内的桶
            if (i >= k) mp.erase(getIdx(nums[i - k]));
        }
        return false;
    }
private:
    LL size;
    LL getIdx(LL u) {
        return u >= 0 ? u / size : ((u + 1) / size) - 1;
    }
};
```

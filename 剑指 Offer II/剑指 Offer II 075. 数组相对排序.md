### [剑指 Offer II 075. 数组相对排序](https://leetcode.cn/problems/0H97ZC/)

### 自定义排序

哈希表存储 `数字->索引`

- 时间复杂度：O(mlogm+n)
    - 构造哈希表 O(n)；排序 O(mlogm)
- 空间复杂度：O(logm+n)
    - 哈希表 O(n)；排序 O(logm)

```c++
class Solution {
public:
    vector<int> relativeSortArray(vector<int>& arr1, vector<int>& arr2) {
        unordered_map<int, int> mp;
        for (int i = 0; i < arr2.size(); i++) mp[arr2[i]] = i;

        sort(arr1.begin(), arr1.end(), [&](int x, int y) {
            // 都出现在 arr2 中，按下标大小比较
            if (mp.count(x)) return mp.count(y) ? mp[x] < mp[y] : true;
            // 优先摆放出现在 arr2 中的元素，否则按大小比较
            else return mp.count(y) ? false : x < y;
        });

        return arr1;
    }
};
```

### 计数排序

优化空间，`int upper = *max_element(arr1.begin(), arr1.end());`

- 时间复杂度：O(m+n+upper)
- 空间复杂度：O(upper)

```c++
class Solution {
public:
    vector<int> relativeSortArray(vector<int>& arr1, vector<int>& arr2) {
        // 对 arr1 计数
        int cnt[1001] = {0};
        for (auto& e : arr1) ++cnt[e];

        vector<int> ans;
        // 按 arr2 的顺序压入
        for (auto& e : arr2) {
            while (0 < cnt[e]--) ans.push_back(e);
        }

        // 剩余没有出现在 arr2 中的元素，按升序压入
        for (int e = 0; e < 1001; e++) {
            while (0 < cnt[e]--) ans.push_back(e);
        }
            
        return ans;
    }
};
```

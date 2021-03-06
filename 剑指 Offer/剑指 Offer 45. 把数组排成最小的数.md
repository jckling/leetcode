### [剑指 Offer 45. 把数组排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

### 排序

- 时间复杂度：O(nlogn)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    string minNumber(vector<int>& nums) {
        vector<string> strs;
        for (auto& num : nums) strs.push_back(to_string(num));
        sort(strs.begin(), strs.end(), [](auto& x, auto& y){ return x + y < y + x; });

        string res;
        for (string s : strs) res.append(s);
        return res;
    }
};
```

手写快排

```c++
class Solution {
public:
    string minNumber(vector<int>& nums) {
        // 暂存数字的字符串
        vector<string> strs;
        for (auto& num : nums) strs.push_back(to_string(num));

        // 按拼接大小排序
        qsort(strs, 0, strs.size() - 1);

        // 拼接字符串
        string res;
        for (auto& s : strs) res.append(s);
        return res;
    }
private:
    void qsort(vector<string>& strs, int l, int r) {
        if (l >= r) return;

        // 哨兵
        int i = l, j = r;
        while (i < j) {
            while (i < j && strs[j] + strs[l] >= strs[l] + strs[j]) j--;
            while (i < j && strs[i] + strs[l] <= strs[l] + strs[i]) i++;
            swap(strs[i], strs[j]);
        }
        swap(strs[i], strs[l]);

        // 递归左右
        qsort(strs, l, i - 1);
        qsort(strs, i + 1, r);
    }
};
```

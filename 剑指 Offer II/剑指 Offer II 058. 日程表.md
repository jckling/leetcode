### [剑指 Offer II 058. 日程表](https://leetcode.cn/problems/fi9suh/)

### 模拟

- 时间复杂度：O(n^2)
- 空间复杂度：O(n)

```c++
class MyCalendar {
public:
    vector<pair<int, int>> calendar;
    MyCalendar() {}
    
    bool book(int start, int end) {
        for (auto& p : calendar) {
            if (p.first < end && start < p.second) return false;
        }
        calendar.emplace_back(start, end);
        return true;
    }
};

/**
 * Your MyCalendar object will be instantiated and called as such:
 * MyCalendar* obj = new MyCalendar();
 * bool param_1 = obj->book(start,end);
 */
```

### 红黑树

- 时间复杂度：O(nlogn)
- 空间复杂度：O(n)

```c++
class MyCalendar {
public:
    map<int, int> mp;
    MyCalendar() {}
    
    bool book(int start, int end) {
        auto lb = mp.lower_bound(start);
        // 当前迭代器存在，其左边界小于日程右边界
        if (lb != mp.end() && lb->first < end) return false;
        // 上一迭代器存在，其右边界大于日程左边界
        if (lb != mp.begin() && (--lb)->second > start) return false;
        mp[start] = end;
        return true;
    }
};
```

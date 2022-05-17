### [剑指 Offer II 035. 最小时间差](https://leetcode.cn/problems/569nqc/)

### 模拟

- 时间复杂度：O(nlogn)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int findMinDifference(vector<string>& timePoints) {
        // 记录 00:00 左右两侧时间，时间可以当作今天的也可以当作明天的
        int n = timePoints.size() * 2;
        vector<int> nums(n);

        for (int i = 0, idx = 0; i < n / 2; i++, idx += 2) {
            string ss = timePoints[i];
            auto pos = ss.find(':');
            int h = stoi(ss.substr(0, pos)), m = stoi(ss.substr(pos + 1));

            // 时间
            nums[idx] = h * 60 + m;             // 今天（左侧）
            nums[idx + 1] = nums[idx] + 1440;   // 明天（右侧）
        }

        // 从小到大排序
        sort(nums.begin(), nums.end());
        int ans = nums[1] - nums[0];
        for (int i = 0; i < n - 1; i++) {
            ans = min(ans, nums[i + 1] - nums[i]);  // 差值最小
        }

        return ans;
    }
};
```

### 数学

抽屉原理

- 时间复杂度：O(C)
- 空间复杂度：O(C)

```c++
class Solution {
public:
    int findMinDifference(vector<string>& timePoints) {
        // 一天最多 1440 个时间点
        int n = timePoints.size();
        if (n >= 1440) return 0;

        // 哈希（桶）
        vector<int> cnts(1440 * 2 + 10);
        for (auto ss : timePoints) {
            auto pos = ss.find(':');
            int h = stoi(ss.substr(0, pos)), m = stoi(ss.substr(pos + 1));
            cnts[h * 60 + m]++;
            cnts[h * 60 + m + 1440]++;  // 第二天
        }

        // 从小到大遍历
        int ans = 1440, last = -1;
        for (int i = 0; i <= 1440 * 2 && ans != 0; i++) {
            if (cnts[i] == 0) continue;
            if (cnts[i] > 1) ans = 0;
            else if (last != -1) ans = min(ans, i - last);  // 分钟
            last = i;
        }
  
        return ans;
    }
};
```
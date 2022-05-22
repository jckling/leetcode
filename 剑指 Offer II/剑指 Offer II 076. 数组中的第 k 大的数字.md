### [剑指 Offer II 076. 数组中的第 k 大的数字](https://leetcode.cn/problems/xx4gT2/)

### 小根堆

优先队列

- 时间复杂度：O(nlogn)
	- 建堆 O(n)，删除 O(klogn)
- 空间复杂度：O(logn)

```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int, vector<int>, greater<int>> q;
        for (int i = 0; i < k; i++) {
            if (i == nums.size()) return q.top();
            q.push(nums[i]);
        }

        for (int i = k; i < nums.size(); i++) {
            q.push(nums[i]);
            q.pop();
        }
        return q.top();
    }
};
```

### 快排

- 时间复杂度：O(n)
- 空间复杂度：O(logn)

```c++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        srand(time(0));
        return quickSelect(nums, 0, nums.size() - 1, nums.size() - k);
    }
private:
    // 排序
    int partition(vector<int>& nums, int l, int r) {
        int x = nums[r], i = l - 1;
        for (int j = l; j < r; j++) {
            if (nums[j] <= x) swap(nums[++i], nums[j]);
        }
        swap(nums[i + 1], nums[r]);
        return i + 1;   // 排序定点 pivot
    }

    // 随机交换
    int randomPartition(vector<int>& nums, int l, int r) {
        int i = rand() % (r - l + 1) + l;
        swap(nums[i], nums[r]);
        return partition(nums, l, r);
    }

    int quickSelect(vector<int>& nums, int l, int r, int idx) {
        int q = randomPartition(nums, l, r);
        if (q == idx) return nums[q];
        return q < idx ? quickSelect(nums, q + 1, r, idx) : quickSelect(nums, l, q - 1, idx);
    }
};
```

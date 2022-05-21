### [剑指 Offer II 059. 数据流的第 K 大数值](https://leetcode.cn/problems/jBjn9C/)

### 小根堆

优先队列

- 时间复杂度：O(nlogk)
- 空间复杂度：O(logk)

```c++
class KthLargest {
public:
    priority_queue<int, vector<int>, greater<int>> q;
    int k;
    KthLargest(int _k, vector<int>& nums) : k(_k) {
        for (auto& num : nums) add(num);
    }
    
    int add(int val) {
        q.push(val);
        if (q.size() > k) q.pop();  // 弹出最小值
        return q.top();
    }
};

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest* obj = new KthLargest(k, nums);
 * int param_1 = obj->add(val);
 */
```

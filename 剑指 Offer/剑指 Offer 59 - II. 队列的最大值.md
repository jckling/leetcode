### [剑指 Offer 59 - II. 队列的最大值](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

### 双端队列

- 时间复杂度：O(1)
- 空间复杂度：O(n)

```c++
class MaxQueue {
public:
    queue<int> q;
    deque<int> dq;  // 单调递减
    MaxQueue() { }
    
    int max_value() {
        return dq.empty() ? -1 : dq.front();
    }
    
    void push_back(int value) {
        q.push(value);
        while (!dq.empty() && dq.back() < value) dq.pop_back();
        dq.push_back(value);
    }
    
    int pop_front() {
        if (q.empty()) return -1;
        
        int val = q.front();
        q.pop();
        if (dq.front() == val) dq.pop_front();

        return val;
    }
};

/**
 * Your MaxQueue object will be instantiated and called as such:
 * MaxQueue* obj = new MaxQueue();
 * int param_1 = obj->max_value();
 * obj->push_back(value);
 * int param_3 = obj->pop_front();
 */
```

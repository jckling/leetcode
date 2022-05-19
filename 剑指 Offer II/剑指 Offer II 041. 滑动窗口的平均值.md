### [剑指 Offer II 041. 滑动窗口的平均值](https://leetcode.cn/problems/qIsx9U/)

### 队列

- 时间复杂度：O(n)
- 空间复杂度：O(size)

```c++
class MovingAverage {
public:
    /** Initialize your data structure here. */
    queue<int> q;
    int sum = 0;
    int size;

    MovingAverage(int _size) : size(_size) {}
    
    double next(int val) {
        q.push(val);
        sum += val;
        if (q.size() > size) {
            sum -= q.front();
            q.pop();
        }
        
        return 1.0 * sum / q.size();
    }
};

/**
 * Your MovingAverage object will be instantiated and called as such:
 * MovingAverage* obj = new MovingAverage(size);
 * double param_1 = obj->next(val);
 */
```

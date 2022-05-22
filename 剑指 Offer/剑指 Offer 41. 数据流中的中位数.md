### [剑指 Offer 41. 数据流中的中位数](https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/)

### 堆

优先队列

- 时间复杂度：查找 O(1)；添加 O(logn)
- 空间复杂度：O(n)

```c++
class MedianFinder {
public:
    // 小根堆，保存较大的一半
    priority_queue<int, vector<int>, greater<int>> A;
    
    // 大根堆，保存较小的一半
    priority_queue<int, vector<int>, less<int>> B;
    
    MedianFinder() {}
    
    void addNum(int num) {
        // 奇数个数 -> 偶数
        if (A.size() != B.size()) {
            A.push(num);    // 最大里最小的移到 B
            B.push(A.top());
            A.pop();
        }

        // 偶数个数 -> 奇数
        else {
            B.push(num);    // 最小里最大的移到 A
            A.push(B.top());
            B.pop();
        }
    }
    
    double findMedian() {
        if (A.size() != B.size()) return A.top();
        return (A.top() + B.top()) / 2.0;
    }
};

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
```

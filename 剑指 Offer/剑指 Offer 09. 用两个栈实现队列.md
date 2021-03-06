### [剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

### 栈

- 时间复杂度：`appendTail()` O(1)；`deleteHead()` O(n)
- 空间复杂度：O(n)

```c++
class CQueue {
public:
    stack<int> A;
    stack<int> B;

    CQueue() {
    }
    
    void appendTail(int value) {
        A.push(value);
    }
    
    int deleteHead() {
        if(B.empty()) {
            while(!A.empty()) {
                B.push(A.top());
                A.pop();
            }
        }

        if(B.empty()) return -1;
        else{
            int res = B.top();
            B.pop();
            return res;
        }
    }
};

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue* obj = new CQueue();
 * obj->appendTail(value);
 * int param_2 = obj->deleteHead();
 */
 ```
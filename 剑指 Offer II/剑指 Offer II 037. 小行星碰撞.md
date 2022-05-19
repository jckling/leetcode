### [剑指 Offer II 037. 小行星碰撞](https://leetcode.cn/problems/XagZNi/)

### 栈

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    vector<int> asteroidCollision(vector<int>& asteroids) {
        vector<int> ans;
        for (auto& n :asteroids) {
            // 正数入栈
            if (ans.empty() || n > 0) ans.push_back(n);
            else {
                // 栈顶小于飞来的行星
                while (ans.size() && ans.back() > 0 && ans.back() < -n) ans.pop_back();
                // 栈为空、栈顶小于零（负数入栈）
                if (ans.empty() || ans.back() < 0) ans.push_back(n);
                // 栈顶和飞来的行星同时爆炸
                else if (ans.back() == -n) ans.pop_back();
            }
        }

        // 结果全为正数或负数
        return ans;
    }
};
```

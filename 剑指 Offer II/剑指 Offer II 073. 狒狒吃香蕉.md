### [剑指 Offer II 073. 狒狒吃香蕉](https://leetcode.cn/problems/nZZqjQ/)

### 二分

- 时间复杂度：O(nlog(max(piles)))
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int h) {
        int imax = 0;
        for (auto& pile : piles) imax = max(imax, pile);

        int l = 1, r = imax;
        while (l < r) {
            int m = l + (r - l) / 2;
            if (cal(piles, m) > h) l = m + 1;
            else r = m;
        }
        return l;
    }
private:
    int cal(vector<int>& piles, int speed) {
        int tot = 0;    // 向上取整
        for (auto& pile : piles) tot += (pile - 1) / speed + 1;
        return tot;
    }
};
```

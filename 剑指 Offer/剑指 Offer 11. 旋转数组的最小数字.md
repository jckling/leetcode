### [旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

### 二分

- 时间复杂度：O(logn)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    int minArray(vector<int>& numbers) {
        int l = 0, r = numbers.size() - 1;
        while (l < r) {
            int m = (l + r) / 2;
            if (numbers[m] > numbers[r]) l = m + 1;
            else if (numbers[m] < numbers[r]) r = m;
            else r--;
        }
        return numbers[l];
    }
};
```

### [剑指 Offer 58 - II. 左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

### 遍历

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    string reverseLeftWords(string s, int n) {
        string ans;
        int len = s.size();
        for (int i = 0; i < len; i++) {
            ans += s[(i + n) % len];
        }
        return ans;
    }
};
```

### 数学

三次翻转

- 时间复杂度：O(n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    string reverseLeftWords(string s, int n) {
        // n=2, abcd -> bacd
        reverse(s.begin(), s.begin() + n);

        // bacd -> badc
        reverse(s.begin() + n, s.end());

        // badc -> cdab
        reverse(s.begin(), s.end());
        
        return s;
    }
};
```

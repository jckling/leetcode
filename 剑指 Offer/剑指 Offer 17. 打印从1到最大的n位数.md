### [剑指 Offer 17. 打印从 1 到最大的 n 位数](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)

### 遍历

- 时间复杂度：O(10^n)
- 空间复杂度：O(1)

```c++
class Solution {
public:
    vector<int> printNumbers(int n) {
        vector<int> ans;
        for (int i = 1; i < pow(10, n); i++) ans.emplace_back(i);
        return ans;
    }
};
```

### DFS

全排列

- 时间复杂度：O(10^n)
- 空间复杂度：O(10^n)

```c++
class Solution {
public:
    vector<int> printNumbers(int n) {
        dfs(n, 0, "");
        vector<int> ans;
        for(string s : res) ans.push_back(stoi(s));
        return ans;
    }
private:
    vector<string> res;
    void dfs(int n, int cnt, string s) {
        if (cnt == n) {
            if(s.front() != '0') res.push_back(s);
            return;
        }

        for (int i = 0; i <= 9; i++) {
            if (s.size() && s.front() == '0') dfs(n, cnt + 1, to_string(i));
            else dfs(n, cnt + 1, s + to_string(i));
        }
    }
};
```

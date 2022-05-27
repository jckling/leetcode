### [剑指 Offer II 117. 相似的字符串](https://leetcode.cn/problems/H6lPxb/)

### 并查集

- 时间复杂度：$O(n^2m + n \log n)$
    - n 表示字符串数量，m 表示检查相似性
- 空间复杂度：O(n)

```c++
class Solution {
public:
    int numSimilarGroups(vector<string>& strs) {
        int n = strs.size();
        init(n);

        int m = strs[0].length();
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int pi = find(i), pj = find(j);
                if (pi == pj) continue;
                if (check(strs[i], strs[j], m)) p[pi] = pj;
            }
        }

        int ans = 0;
        for (int i = 0; i < n; i++) {
            if (p[i] == i) ans++;
        }
        return ans;
    }
private:
    vector<int> p;
    void init(int n) {
        p.resize(n + 1);
        for (int i = 1; i <= n; i++) p[i] = i;
    }

    int find(int x) {
        if (p[x] != x) p[x] = find(p[x]);
        return p[x];
    }

    bool check(string& a, string& b, int len) {
        int diff = 0;
        for (int i = 0; i < len; i++) {
            if (a[i] != b[i]) {
                diff++;
                if (diff > 2) return false;
            }
        }
        return true;
    }
};
```

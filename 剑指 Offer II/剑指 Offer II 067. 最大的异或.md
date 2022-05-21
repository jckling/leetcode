### [剑指 Offer II 067. 最大的异或](https://leetcode.cn/problems/ms70jA/)

### 前缀树

- 时间复杂度：O(nlogC)
- 空间复杂度：O(nlogC)
    - n 表示数组长度
    - C 表示数字范围

```c++
class Trie {
private:
    Trie* next[2] = { nullptr };
public:
    Trie() {}

    void insert(int x) {
        Trie* root = this;
        for (int i = 30; i >= 0; i--) {
            int u = (x >> i) & 1; // 取第 i 位的数字，30...0
            if (root->next[u] == nullptr) root->next[u] = new Trie();
            root = root->next[u];
        }
    }

    int search(int x) {
        Trie* root = this;
        int res = 0;
        for (int i = 30; i >= 0; i--) {
            int u = (x >> i) & 1;
            // 若 x 的第 u 位存在，走到相反的方向去，异或总是值相反取最大值
            if(root->next[!u]) {
                root = root->next[!u];
                res = res * 2 + !u; // 左移一位，加上当前最低位数字
            }
            // 相反方向的节点为空，只能顺着相同方向走
            else {
                root=root->next[u];
                res = res * 2 + u;
            }
        }
        // 两个数的最大异或值
        res ^= x;
        return res;
    }
};

class Solution {
public:
    int findMaximumXOR(vector<int>& nums) {
        Trie* root = new Trie();
        for (auto& num : nums) root->insert(num);
        int res = 0;
        for (auto& num : nums) res = max(res, root->search(num));
        return res;
    }
};
```

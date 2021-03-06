### [剑指 Offer 12. 矩阵中的路径](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)

### DFS

- 时间复杂度：O((3^k)*mn)
    - k 表示字符串长度，方案数量 3^k
- 空间复杂度：O(K)

```c++
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        for (int i = 0; i < board.size(); i++) {
            for (int j = 0; j < board[0].size(); j++) {
                if (dfs(board, word, 0, i, j)) return true;
            }
        }
        return false;
    }
private:
    bool dfs(vector<vector<char>>& board, string& word, int idx, int x, int y) {
        if (x < 0 || x >= board.size() || y < 0 || y >= board[0].size() || board[x][y] != word[idx]) return false;

        if (idx == word.size() - 1) return true;

        board[x][y] = '\0';
        bool res = dfs(board, word, idx + 1, x + 1, y)   ||
                    dfs(board, word, idx + 1, x , y + 1) || 
                    dfs(board, word, idx + 1, x - 1, y)  ||
                    dfs(board, word, idx + 1, x, y - 1);
        board[x][y] = word[idx];
        return res;
    }
};
```

### [剑指 Offer II 013. 二维子矩阵的和](https://leetcode.cn/problems/O4NDxx/)

### 二维前缀和

- 时间复杂度：O(mn)
- 空间复杂度：O(mn)

```c++
class NumMatrix {
public:
    vector<vector<int>> sum;    // 二维前缀和
    NumMatrix(vector<vector<int>>& matrix) {
        int m = matrix.size(), n = m == 0 ? 0 : matrix[0].size();
        sum.resize(m + 1, vector<int>(n + 1, 0));

        // 预处理（容斥原理）
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                sum[i][j] = sum[i - 1][j] + sum[i][j - 1] - sum[i - 1][j - 1] + matrix[i - 1][j - 1];
            }
        }
    }
    
    int sumRegion(int row1, int col1, int row2, int col2) {
        row1++;
        col1++;
        row2++;
        col2++;
        return sum[row2][col2] - sum[row1 - 1][col2] - sum[row2][col1 - 1] + sum[row1 - 1][col1 - 1];
    }
};

/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix* obj = new NumMatrix(matrix);
 * int param_1 = obj->sumRegion(row1,col1,row2,col2);
 */
```

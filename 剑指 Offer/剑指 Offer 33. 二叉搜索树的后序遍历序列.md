### [剑指 Offer 33. 二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

### 递归

- 时间复杂度：O(n^2)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    // 后序遍历：左右根
    // postorder = [<root, >root, root]
    bool verifyPostorder(vector<int>& postorder) {
        return recur(postorder, 0, postorder.size() - 1);
    }
private:
    bool recur(vector<int>& postorder, int i, int j) {
        if (i >= j) return true;

        // 左 <root
        int p = i;
        while (postorder[p] < postorder[j]) p++;
        
        // 右 >root
        int m = p;
        while (postorder[p] > postorder[j]) p++;

        return p == j && recur(postorder, i, m - 1) && recur(postorder, m, j - 1);
    }
};
```

### 单调栈

根右左倒序遍历

- 时间复杂度：O(n)
- 空间复杂度：O(n)

```c++
class Solution {
public:
    // 后序遍历：左右根
    // postorder = [<root, >root, root]
    bool verifyPostorder(vector<int>& postorder) {
        stack<int> stk; // 单调递增
        int root = INT_MAX;

        // 倒序遍历：根右左
        for (int i = postorder.size() - 1; i >= 0; i--) {
            if (postorder[i] > root) return false;

            // 左 <root
            while (!stk.empty() && stk.top() > postorder[i]) {
                root = stk.top();   // 更新
                stk.pop();
            }

            stk.push(postorder[i]);
        }

        return true;
    }
};
```

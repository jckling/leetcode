### [剑指 Offer II 108. 单词演变](https://leetcode.cn/problems/om3reC/)

### BFS

双向 BFS，对单词的字符进行替换，若在单词表中则可以进行转换。

- 时间复杂度：$O(n \times c^2)$
    -  n 表示 `wordList` 的长度，c 表示列表中单词的长度
- 空间复杂度：$O(n \times c^2)$

```c++
class Solution {
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        // 集合（去重）
        unordered_set<string> words(wordList.begin(), wordList.end());

        // 特殊情况
        if (words.empty() || words.find(endWord) == words.end()) return 0;

        // 移除开始单词、结束单词
        words.erase(beginWord);
        words.erase(endWord);

        // 访问标记
        unordered_set<string> beginVisited;
        beginVisited.insert(beginWord);
        unordered_set<string> endVisited;
        endVisited.insert(endWord);

        int step = 1;
        while (!beginVisited.empty() && !endVisited.empty()) {
            // 优先扩散小的集合
            if (beginVisited.size() > endVisited.size()) beginVisited.swap(endVisited);
            // 下一层集合
            unordered_set<string> nextVisited;
            for (string s : beginVisited) {
                for (int i = 0; i < s.size(); i++) {
                    char c = s[i];
                    for (int j = 0; j < 26; j++) {
                        if ('a' + j == c) continue;
                        s[i] = 'a' + j;
                        // 相遇
                        if (endVisited.find(s) != endVisited.end()) return step + 1;
                        // 未相遇，但在单词表中
                        if (words.find(s) != words.end()) {
                            nextVisited.insert(s);
                            words.erase(s);         // 访问过
                        }
                    }
                    s[i] = c;
                }
            }
            beginVisited = nextVisited;
            step++;
        }

        return 0;
    }
};
```

### [剑指 Offer II 065. 最短的单词编码](https://leetcode.cn/problems/iSwD2y/)

### 哈希表

- 时间复杂度：O(∑w^2)
- 空间复杂度：O(∑w)

```c++
class Solution {
public:
    int minimumLengthEncoding(vector<string>& words) {
        unordered_set<string> st(words.begin(), words.end());
        for (auto& word : words) {
            for (int i = 1; i < word.size(); i++) st.erase(word.substr(i)); // 删除前缀
        }

        int len = 0;
        for (auto& word : st) len += word.size() + 1;

        return len;
    }
};
```

### 前缀树

- 时间复杂度：O(nlogn)?
- 空间复杂度：O(s\*∑w)
    - s 表示字符集大小

```c++
class Trie {
private:
    bool isEnd;
    vector<Trie*> next;
public:
    /** Initialize your data structure here. */
    Trie() {
        isEnd = false;
        next.resize(26);
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        Trie* node = this;
        for (auto& c : word) {
            int idx = c - 'a';
            if (node->next[idx] == nullptr) node->next[idx] = new Trie();
            node = node->next[idx];
        }
        node->isEnd = true;
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        Trie* node = this;
        for (auto& c : word) {
            int idx = c - 'a';
            if (node->next[idx] == nullptr) return false;
            node = node->next[idx];
        }
        return node->isEnd;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        Trie* node = this;
        for (auto& c : prefix) {
            int idx = c - 'a';
            if (node->next[idx] == nullptr) return false;
            node = node->next[idx];
        }
        return true;
    }
};

class Solution {
public:
    int minimumLengthEncoding(vector<string>& words) {
        // 按字符串长度排序
        auto cmp = [&](string& a, string& b) {
            return a.size() > b.size();
        };
        sort(words.begin(), words.end(), cmp);

        // 前缀树
        Trie* root = new Trie();
        int len = 0;
        for (auto& word : words) {
            string s(word);
            reverse(s.begin(), s.end());    // 反过来插入，过滤后缀
            if (root->startsWith(s)) continue;
            root->insert(s);
            len += s.size() + 1;
        }
        return len;
    }
};
```

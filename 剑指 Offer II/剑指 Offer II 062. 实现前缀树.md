### [剑指 Offer II 062. 实现前缀树](https://leetcode.cn/problems/QC3q1f/)

### 前缀树

- 时间复杂度：初始化 O(1)；其余操作 O(|S|)，字符长度
- 空间复杂度：O(|T|\*Σ)，字符长度之和、字符集大小

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

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```

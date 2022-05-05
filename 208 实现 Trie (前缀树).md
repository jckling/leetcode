## 多叉树

- 时间复杂度：初始化 O(1)；其余操作 O(|S|)，字符长度
- 空间复杂度：O(|T|\*Σ)，字符长度之和、字符集大小

```c++
class Trie {
private:
    bool isEnd;         // 是否为一个串的结束
    vector<Trie*> next; // 字母映射表，指向子节点
public:
    Trie() {
        isEnd = false;
        next.resize(26);
    }
    
    // 插入字符后将最后一个节点的 isEnd 置为 true`，表示单词末尾
    void insert(string word) {
        Trie* node = this;
        for (auto& c : word) {
            int idx = c - 'a';
            if (node->next[idx] == nullptr) node->next[idx] = new Trie();
            node = node->next[idx];
        }
        node->isEnd = true;
    }
    
    // 从根节点的子节点开始向下匹配
    bool search(string word) {
        Trie* node = this;
        for (auto& c : word) {
            int idx = c - 'a';
            if (node->next[idx] == nullptr) return false;
            node = node->next[idx];
        }
        return node->isEnd;
    }
    
    // 和查找类似，不需要判断 isEnd
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

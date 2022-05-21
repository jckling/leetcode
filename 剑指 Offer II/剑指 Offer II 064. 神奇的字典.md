### [剑指 Offer II 064. 神奇的字典](https://leetcode.cn/problems/US1pGT/)

### 广义邻居（集合 + 哈希表）

- 时间复杂度：构建字典 O(∑w^2)；搜索 O(k^2)
    - w 表示单词长度，k 表示搜索单词的长度
- 空间复杂度：O(∑w^2)

```c++
class MagicDictionary {
public:
    /** Initialize your data structure here. */
    MagicDictionary() { }    
    void buildDict(vector<string> dictionary) {
        for (auto& s : dictionary) {
            st.insert(s);
            for (auto& neighbor : getNeighbors(s)) mp[neighbor]++;
        }
    }
    
    // 查找是否存在广义邻居：只有一个字母不同的单词
    bool search(string searchWord) {
        for (auto& neighbor : getNeighbors(searchWord)) {
            int cnt = 0;
            if (mp.find(neighbor) != mp.end()) cnt = mp[neighbor];
            if (cnt > 1 || cnt == 1 && !st.count(searchWord)) return true;
        }
        return false;
    }
private:
    unordered_set<string> st;       // 单词
    unordered_map<string, int> mp;  // 广义邻居个数
    // 生成单词的所有广义邻居
    vector<string> getNeighbors(string word) {
        int n = word.size();
        vector<string> neighbors(n);
        for (int i = 0; i < n; i++) {
            char c = word[i];
            word[i] = '*';
            neighbors[i] = word;
            word[i] = c;
        }
        return neighbors;
    }
};

/**
 * Your MagicDictionary object will be instantiated and called as such:
 * MagicDictionary* obj = new MagicDictionary();
 * obj->buildDict(dictionary);
 * bool param_2 = obj->search(searchWord);
 */
```

### 前缀树（超时）

- 时间复杂度：O(n)
- 空间复杂度：O(n)

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
};

class MagicDictionary {
public:
    Trie* root;
    /** Initialize your data structure here. */
    MagicDictionary() {
        root = new Trie();
    }
    
    void buildDict(vector<string> dictionary) {
        for (auto& s : dictionary) root->insert(s);
    }
    
    bool search(string searchWord) {
        for (int i = 0; i < searchWord.size(); i++) {
            for (int idx = 0; idx < 26; idx++) {
                char c = 'a' + idx;
                if (searchWord[i] != c) {
                    string s = searchWord;
                    s[i] = c;
                    if (root->search(s)) return true;
                }
            }
        }

        return false;
    }
};
```

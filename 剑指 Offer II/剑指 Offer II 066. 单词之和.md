### [剑指 Offer II 066. 单词之和](https://leetcode.cn/problems/z1R5dt/)

### 哈希表

前缀哈希

- 时间复杂度：插入 O(n^2)；查询 O(1)
- 空间复杂度：O(mn)
    - m 表示键值对数量
    - n 表示 key 长度

```c++
class MapSum {
public:
    unordered_map<string, int> mp;          // k-v
    unordered_map<string, int> prefixmap;   // 前缀和
    /** Initialize your data structure here. */
    MapSum() {}
    
    void insert(string key, int val) {
        int delta = val;                        // 不存在，更新值
        if (mp.count(key)) delta -= mp[key];    // 存在，更新差值
        mp[key] = val;
        // 更新前缀和
        for (int i = 1; i <= key.size(); i++) {
            prefixmap[key.substr(0, i)] += delta;
        }
    }
    
    int sum(string prefix) {
        return prefixmap[prefix];
    }
};

/**
 * Your MapSum object will be instantiated and called as such:
 * MapSum* obj = new MapSum();
 * obj->insert(key,val);
 * int param_2 = obj->sum(prefix);
 */
```

### 前缀树

- 时间复杂度：插入 O(n)；查询 O(n)
- 空间复杂度：O(mn)


```c++
struct TrieNode {
    int val;
    TrieNode* next[26];
    TrieNode() {
        this->val = 0;
        for (int i = 0; i < 26; i++) {
            this->next[i] = nullptr;
        }
    }
};

class MapSum {
private:
    TrieNode* root;
    unordered_map<string, int> mp;  // k-v
public:
    /** Initialize your data structure here. */
    MapSum() {
        root = new TrieNode();
    }
    
    void insert(string key, int val) {
        int delta = val;                        // 不存在，更新值
        if (mp.count(key)) delta -= mp[key];    // 存在，更新差值
        mp[key] = val;
        TrieNode* node = root;
        for (auto& c : key) {
            if (node->next[c - 'a'] == nullptr) {
                node->next[c - 'a'] = new TrieNode();
            }
            node = node->next[c - 'a'];
            node->val += delta; // 更新
        }
    }
    
    int sum(string prefix) {
        TrieNode * node = root;
        for (auto& c : prefix) {
            if (node->next[c - 'a'] == nullptr) return 0;
            node = node->next[c - 'a'];
        }
        return node->val;
    }
};
```

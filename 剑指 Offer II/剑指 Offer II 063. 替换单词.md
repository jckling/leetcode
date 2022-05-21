### [剑指 Offer II 063. 替换单词](https://leetcode.cn/problems/UhWRSj/)

### 哈希表

前缀哈希

- 时间复杂度：O(∑w^2)
    - w 表示单词长度
- 空间复杂度：O(n)

```c++
class Solution {
public:
    string replaceWords(vector<string>& dictionary, string sentence) {
        // 集合存储词根
        unordered_set<string> st;
        for (auto& s : dictionary) st.insert(s);

        string ans = "";
        istringstream iss(sentence);
        string word, prefix;

        // 分割单词
        while (getline(iss, word, ' ')) {
            // 截取字符串
            for (int i = 0; i <= word.size(); i++) {
                prefix = word.substr(0, i);
                if (st.find(prefix) != st.end()) break;
            }
            if (ans.size() > 0) ans.append(" ");
            ans.append(prefix);
        }

        return ans;
    }
};
```

### 前缀树

- 时间复杂度：O(n)
    - n 表示句子长度
- 空间复杂度：O(n)

```c++
class Trie {
private:
    bool isEnd;
    vector<Trie*> next;
public:
    Trie() {
        isEnd = false;
        next.resize(26);
    }
    
    void insert(string word) {
        Trie* node = this;
        for (auto& c : word) {
            int idx = c - 'a';
            if (node->next[idx] == nullptr) node->next[idx] = new Trie();
            node = node->next[idx];
        }
        node->isEnd = true;
    }
    
    string find(string word) {
        string s;
        Trie* node = this;
        for (auto& c : word) {
            int idx = c - 'a';
            if (node->next[idx] == nullptr) break;
            else {
                s += c;
                node = node->next[idx];
            }
            if (node->isEnd) return s;  // 提前返回
        }
        return node->isEnd ? s : "";
    }
};

class Solution {
public:
    string replaceWords(vector<string>& dictionary, string sentence) {
        string ans;
        istringstream iss(sentence);
        string word, prefix;
        
        Trie* root = new Trie();
        for (auto& s : dictionary) root->insert(s);
        
        while(getline(iss, word, ' ')) {
            string prefix = root->find(word);
            if (prefix.size()) ans.append(prefix);
            else ans.append(word);
            ans.append(" ");
        }

        return ans.substr(0, ans.size() - 1);
    }
};
```

---
created:
  - 2023-07-08 18:49
share: true
---

up::[Tries](NeetCode%20Index.md#^4a0214)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
>- Design a data structure that supports adding new words and finding if a string matches any previously added string.
> 
> - Implement the `WordDictionary` class:
> 
> - `WordDictionary()` Initializes the object.
> - `void addWord(word)` Adds `word` to the data structure, it can be matched later.
> - `bool search(word)` Returns `true` if there is any string in the data structure that matches `word` or `false` otherwise. `word` may contain dots `'.'` where dots can be matched with any letter.
> 
> ![Pasted image 20230708185044.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230708185044.png)
> 
> **Constraints:**
> 
> - `1 <= word.length <= 25`
> - `word` in `addWord` consists of lowercase English letters.
> - `word` in `search` consist of `'.'` or lowercase English letters.
> - There will be at most `2` dots in `word` for `search` queries.
> - At most `104` calls will be made to `addWord` and `search`.

## 🔑 **Key Points of Understanding**
- We use a trie.
- When we encounter a "." , we need to search through all the children with the rest of the word.

# 🔍 Solutions

```C++
class WordDictionary {  
private:  
    TrieNode root;  
    bool search_helper(TrieNode* node, string word){  
        TrieNode* cn = node;  
        for(int i = 0 ; i < word.size(); ++i){  
            char c = word[i];  
            if(c == '.') {  
                bool result = false;  
                int size = cn->getSize();  
                TrieNode **children = cn->getChildren();  
                for (int j = 0; j < size && !result; ++j) {  
                    if (children[j]) {  
                        result |= search_helper(children[j], word.substr(i + 1));  
                    }  
                }  
                return result;  
            }else if(!cn->exists(c)){  
                    return false;  
            }else{  
                cn = cn->getChild(c);  
            }  
        }  
        return cn->isAWord();  
    }  
public:  
    WordDictionary() {  
  
    }  
  
    void addWord(string word) {  
        TrieNode* cn = &root;  
        for(auto& c: word){  
            if(!cn->exists(c)){  
                cn->addChild(c);  
            }  
            cn = cn->getChild(c);  
        }  
        cn->markWordEnding();  
    }  
  
    bool search(string word) {  
        return search_helper(&root,word);  
    }  
};
```

# 🧠 Ideas about Problem

# 🔗 Related Applications


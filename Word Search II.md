---
created: ["2023-07-08 21:47"]
share: true
---

up::

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> > Given an `m x n` `board` of characters and a list of strings `words`, return _all words on the board_.
> 
> Each word must be constructed from letters of sequentially adjacent cells, where **adjacent cells** are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.
> 
> 
> ![Pasted image 20230708214756.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230708214756.png)
> 
> **Constraints:**
> 
> - `m == board.length`
> - `n == board[i].length`
> - `1 <= m, n <= 12`
> - `board[i][j]` is a lowercase English letter.
> - `1 <= words.length <= 3 * 104`
> - `1 <= words[i].length <= 10`
> - `words[i]` consists of lowercase English letters.
> - All the strings of `words` are unique.

## 🔑 **Key Points of Understanding**
- The key idea is each word starts around the table.
- You can create words by inserting into the trie. Start by coordinates around the table and selecting the next one by going left , right, up and down until you have no more path to traverse.

# 🔍 Solutions
```C++
#include<iostream>  
#include<vector>  
#include<string>  
#include<algorithm>  
#include<unordered_set>  
  
using std::cout;  
using std::endl;  
using std::vector;  
using std::string;  
using std::pair;  
using std::unordered_set;  
  
class TrieNode{  
private:  
    int size;  
    TrieNode** children;  
    bool isWordEnding;  
public:  
    TrieNode(const int _size = 26):size(_size),children(new TrieNode*[_size]),isWordEnding(false){  
        for(int i = 0 ; i < size; ++i){  
            children[i] = nullptr;  
        }  
    }  
  
    virtual ~TrieNode(){  
        for(int i = 0; i < size;  ++i){  
            if(nullptr){  
                delete children[i];  
                children[i] = nullptr;  
            }  
        }  
    }  
  
    void markWordEnding(){  
        isWordEnding = true;  
    }  
  
    void unmarkWordEnding(){  
        isWordEnding = false;  
    }  
  
    bool isAWord(){  
        return isWordEnding;  
    }  
  
    void addChild(char c){  
        children[c - 'a'] = new TrieNode();  
    }  
  
    bool deleteChild(char c){  
        if(exists(c)){  
            delete children[c-'a'];  
            children[c-'a'] = nullptr;  
            return true;  
        }  
        return false;  
    }  
  
    TrieNode* getChild(char c){  
        return children[c - 'a'];  
    }  
  
    bool exists(char c){  
        return children[c - 'a'] != nullptr;  
    }  
  
    int getSize(){  
        return size;  
    }  
  
    TrieNode** getChildren(){  
        return children;  
    }  
};  
  
struct pair_hash  
{  
    template <class T1, class T2>  
    std::size_t operator() (const std::pair<T1, T2> &pair) const {  
        return std::hash<T1>()(pair.first) ^ std::hash<T2>()(pair.second);  
    }  
};  
  
class Solution {  
private:  
    //Board  
    typedef vector<vector<char>> Board;  
    //<row, col>  
    typedef pair<int,int> Coordinate;  
    //root node for our trie  
    TrieNode root;  
    //  
    typedef unordered_set<Coordinate,pair_hash> Path;  
private:  
    char getChar(Board& board, const Coordinate& coord){  
        return board[coord.first][coord.second];  
    }  
  
    Coordinate getLeft(const Coordinate& coord){  
        return std::make_pair(coord.first,coord.second-1);  
    }  
  
    Coordinate getRight(const Coordinate& coord){  
        return std::make_pair(coord.first,coord.second+1);  
    }  
  
    Coordinate  getUp(const Coordinate& coord){  
        return std::make_pair(coord.first-1, coord.second);  
    }  
  
    Coordinate  getDown(const Coordinate& coord){  
        return std::make_pair(coord.first+1, coord.second);  
    }  
  
    bool isSafe(Board& board,const Coordinate& coord,Path path){  
        int row =  coord.first;  
        int col =  coord.second;  
        return !path.contains(coord) && (row >= 0 && row < board.size() && col >= 0  
                && col < board[row].size());  
    }  
  
    void add_char(TrieNode* node,Path & path,Board& board, const Coordinate& coord){  
        if(isSafe(board,coord,path)){  
            auto ch = getChar(board,coord);  
            if(!node->exists(ch)){  
                node->addChild(ch);  
            }  
            Path newpath(path);  
            newpath.insert(coord);  
            add_char(node->getChild(ch),newpath,board, getDown(coord));  
            add_char(node->getChild(ch),newpath,board, getUp(coord));  
            add_char(node->getChild(ch),newpath,board, getLeft(coord));  
            add_char(node->getChild(ch),newpath,board, getRight(coord));  
        }  
    }  
  
    void add_word(Board& board, const Coordinate& coord){  
        Path path;  
        add_char(&root,path,board,coord);  
    }  
  
    void add_all_words(Board& board){  
        for(int row = 0;  row < board.size() ; ++row){  
            add_word(board,std::make_pair(row,0));  
            add_word(board,std::make_pair(row,board[row].size()-1));  
        }  
  
        int rows[] = {0,static_cast<int>(board.size()-1)};  
        for(int i=0; i < 2; ++i){  
            for(int j = 1; j<board[rows[i]].size()-1 ; ++j){  
                add_word(board,std::make_pair(rows[i],j));  
            }  
        }  
    }  
  
    bool isPrefix(string& word){  
        TrieNode* node = &root;  
        for(auto & c: word){  
            if(!node->exists(c)){  
                return false;  
            }  
            else{  
                node = node->getChild(c);  
            }  
        }  
        return true;  
    }  
  
public:  
    vector<string> findWords(Board& board, vector<string>& words) {  
        vector<string> result;  
        add_all_words(board);  
        for(auto word:words){  
            if(isPrefix(word)){  
                result.push_back(word);  
            }  
        }  
        return result;  
    }  
};  
  
void word_search_test(){  
    vector<vector<char>> board =  {{'o','a','a','n'},{'e','t','a','e'},{'i','h','k','r'},{'i','f','l','v'}};  
    vector<string> words = {"oath","pea","eat","rain"};  
    Solution s;  
    vector<string> found = s.findWords(board,words);  
    for(auto& w:found){  
        cout << w << endl;  
    }  
}
```
# 🧠 Ideas about Problem

# 🔗 Related Applications


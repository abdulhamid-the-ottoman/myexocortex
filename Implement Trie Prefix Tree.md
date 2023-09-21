---
created: ["2023-07-08 12:08"]
share: true
---

up::[Tries](NeetCode%20Index.md#^4a0214)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> -  A [**trie**](https://en.wikipedia.org/wiki/Trie) (pronounced as "try") or **prefix tree** is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.
> 
> Implement the Trie class:
> 
> - `Trie()` Initializes the trie object.
> - `void insert(String word)` Inserts the string `word` into the trie.
> - `boolean search(String word)` Returns `true` if the string `word` is in the trie (i.e., was inserted before), and `false` otherwise.
> - `boolean startsWith(String prefix)` Returns `true` if there is a previously inserted string `word` that has the prefix `prefix`, and `false` otherwise.
> 
> ![Pasted image 20230708121343.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230708121343.png)
> 
> **Explanation**
> Trie trie = new Trie();
> trie.insert("apple");
> trie.search("apple");   // return True
> trie.search("app");     // return False
> trie.startsWith("app"); // return True
> trie.insert("app");
> trie.search("app");     // return True
> 
> **Constraints:**
> 
> - `1 <= word.length, prefix.length <= 2000`
> - `word` and `prefix` consist only of lowercase English letters.
> - At most `3 * 104` calls **in total** will be made to `insert`, `search`, and `startsWith`.


## 🔑 **Key Points of Understanding**
- TrieNode is key
	- holds an array of self reference for each letter
	- holds a bool value for ending of a word
- Insertion 
	- you insert each letter by creating a new node if it doesn't exist at the children array.
	- once you reach the end of the word, you mark it as a word.
- Search word
	- you go letter by letter till the end, once you reach it, check whether it is a word ending.
- Search prefix.
	- you go letter by letter till the end, if you can reach, prefix exists otherwise it doesn't
- Delete word
	- Case 1 : the deleted word is the prefix of other words
		- once you reach the end of the deleted word, you check whether it has more than 0 children, that means this is a prefix
		- You unmark it as word. and return true.
		![400](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230708184242.png)
	- Case 2: the deleted word has common prefix with other words.
		- this case you keep the last branch and the last character before reaching the deleted word this way you can identify the common path.
		- how do you keep the last branch?
			- you constantly go letter by letter and keep the common path where you have more than 1 words using it.
		![Pasted image 20230708184658.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230708184658.png)
	- Case 3: the deleted word has no common prefix at all.
		- in this case, we can delete it as whole.
		![Pasted image 20230708184824.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230708184824.png)

# 🔍 Solutions
```C++
#include <string>  
#include <vector>  
#include <iostream>  
  
using std::vector;  
using std::string;  
using std::cout;  
using std::endl;  
  
class TrieNode{  
public:  
    /*since we have 26 letters in english*/  
    TrieNode* children[26];  
    bool isAWord;  
  
    TrieNode():isAWord(false){  
        for(int i = 0 ; i < 26 ; ++i){  
            children[i] = nullptr;  
        }  
    }  
  
    virtual ~TrieNode(){  
        for(int i = 0 ; i < 26 ; ++i){  
            if(children[i]){  
                delete children[i];  
                children[i] = nullptr;  
            }  
        }  
    }  
  
    int count(){  
        int cnt = 0 ;  
        for(int i = 0 ; i< 26; ++i){  
            if(!children[i]){  
                cnt++;  
            }  
        }  
        return cnt;  
    }  
  
    void markAsEnding(){  
        isAWord = true;  
    }  
  
    void unmarkAsEnding(){  
        isAWord = false;  
    }  
  
    bool isAWordEnding(){  
        return isAWord;  
    }  
};  
  
class Trie{  
private:  
    TrieNode* root;  
  
    TrieNode* createNewNode(){  
        return new TrieNode();  
    }  
public:  
  
    Trie():root(new TrieNode()){  
    }  
  
    virtual ~Trie(){  
        delete root;  
        root= nullptr;  
    }  
  
    void insert(const string& str){  
        TrieNode* cn = root;  
        for(auto& c: str){  
            int index = c - 'a';  
            //check if the node exists in current tree  
            if(!cn->children[index]){  
                //if it doesn't create a new node for it.  
                cn->children[index] = createNewNode();  
            }  
            //now we have to move to the next node to complete  
            cn = cn->children[index];  
        }  
        cn->markAsEnding();  
    }  
  
    bool isPrefixExist(const string& key){  
        TrieNode* cn = root;  
        for(auto& c:key){  
            int index = c - 'a';  
            if(!cn->children[index]){  
                return false;  
            }  
            cn = cn->children[index];  
        }  
        return true;  
    }  
  
    bool search(const string& key){  
        TrieNode* cn = root;  
        for(auto & c : key){  
            int index = c - 'a';  
            if(!cn->children[index]){  
                return false;  
            }  
            cn=cn->children[index];  
        }  
        return cn->isAWordEnding();  
    }  
  
    bool deleteKey(const string& key){  
        /*There are 3 cases */  
        /*1st case: The deleted word is a prefix of other words in Trie*/            // ex: "an" and "ant" - we delete "an",  we unmark the ending  at "an"        /*2nd case: The deleted word shares a common prefix with other words in Trie*/            // ex: "and" and "ant", we delete "and" they share "an", we unmark the ending at d. delete the "d"        /*3rd case: The deleted word does not share any common prefix with other words in Trie*/            // ex: "geek": delete all nodes.on the path.  
       TrieNode* cn = root;  
       TrieNode* lastbranch = nullptr;  
       char lastchar = '!';  
       for(auto& c: key){  
           int index = c - 'a';  
           if(!cn->children[index]){  
               return false;  
           }  
           else{  
               int child_no = cn->count();  
               /*there are more than 1 words using this path*/  
               if(child_no > 1){  
                   lastbranch = cn;  
                   lastchar = c;  
               }  
               cn = cn->children[index];  
           }  
       }  
  
       int child_no = cn->count();  
       //the deleted word is a prefix of the other words  
       //there are other words using this path       if(child_no > 0){  
           cn->unmarkAsEnding();  
           return true;  
       }  
  
       //there are no other paths using this path  
       if(lastbranch){  
           //last branch had diverging paths an vs axe  
           //we are deleting an and a has 2 words coming out of           //we remove the n branch           delete lastbranch->children[lastchar - 'a'];  
           lastbranch->children[lastchar - 'a'] = nullptr;  
           return true;  
       }  
       else{  
            // this means we have no common prefixes.  
            delete root->children[key[0]];  
            root->children[key[0]] = nullptr;  
            return true;  
       }  
    }  
};  
  
  
void test_trie(){  
    Trie trie;  
    vector<string> inputStrings  
            = { "and", "ant", "do", "geek", "dad", "ball" };  
  
    // number of insert operations in the Trie  
    int n = inputStrings.size();  
  
    for (int i = 0; i < n; i++) {  
        trie.insert(inputStrings[i]);  
    }  
  
    // Stores the strings that we want to search in the Trie  
    vector<string> searchQueryStrings  
            = { "do", "geek", "bat" };  
  
    // number of search operations in the Trie  
    int searchQueries = searchQueryStrings.size();  
  
    for (int i = 0; i < searchQueries; i++) {  
        cout << "Query String: " << searchQueryStrings[i]  
             << "\n";  
        if (trie.search(searchQueryStrings[i])) {  
            // the queryString is present in the Trie  
            cout << "The query string is present in the "  
                    "Trie\n";  
        }  
        else {  
            // the queryString is not present in the Trie  
            cout << "The query string is not present in "  
                    "the Trie\n";  
        }  
    }  
  
    // stores the strings that we want to delete from the  
    // Trie    vector<string> deleteQueryStrings = { "geek", "tea" };  
  
    // number of delete operations from the Trie  
    int deleteQueries = deleteQueryStrings.size();  
  
    for (int i = 0; i < deleteQueries; i++) {  
        cout << "Query String: " << deleteQueryStrings[i]  
             << "\n";  
        if (trie.deleteKey(deleteQueryStrings[i])) {  
            // The queryString is successfully deleted from  
            // the Trie            cout << "The query string is successfully "  
                    "deleted\n";  
        }  
        else {  
            // The query string is not present in the Trie  
            cout << "The query string is not present in "  
                    "the Trie\n";  
        }  
    }  
}
```

# 🧠 Ideas about Problem

# 🔗 Related Applications


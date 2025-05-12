---
created:
  - 2023-06-29 21:14
share: true
---

up::

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Given the `head` of a singly linked list, reverse the list and return the reversed list. 
> Example 1: 
>![Pasted image 20230629211718.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230629211718.png)
>**Input:** head = [1,2,3,4,5]
 >**Output:** [5,4,3,2,1]

## 🔑 **Key Points of Understanding**
- You can do this the recursive way as shown in the $1^{st}$ Solution.



# 🔍 Solutions
## $1^{st}$ Solution
```C++
#include <iostream>  
 struct ListNode {  
      int val;  
      ListNode *next;  
      ListNode() : val(0), next(nullptr) {}  
      ListNode(int x) : val(x), next(nullptr) {}  
      ListNode(int x, ListNode *next) : val(x), next(next) {}  
};  
  
class Solution{  
public:  
    ListNode* reverseList(ListNode* head){  
        ListNode* reversed= nullptr;  
        reverse_helper(nullptr,head,&reversed);  
        return reversed;  
    }  
  
  
    void print(ListNode* node){  
        if(node == nullptr){  
            return;  
        }  
        else{  
            std:: cout << node->val << " , " ;  
            print(node->next);  
        }  
    }  
  
private:  
    ListNode* reverse_helper(ListNode* prev, ListNode* current,ListNode** reversed){  
        if(current == nullptr){  
            *reversed = prev;  
            return prev;  
        }  
        else{  
            ListNode* node = reverse_helper(current,current->next,reversed);  
            node->next = prev;  
            return prev;  
        }  
    }  
  
};
```


## $2^{nd}$ Solution

```C++
ListNode* reverseList(ListNode* head){  
    return reverse_iterative(head);  
}
ListNode* reverse_iterative(ListNode* node){  
    ListNode * prev = nullptr;  
    ListNode * next = nullptr;  
    while(node != nullptr){  
        next = node->next;  
        node->next = prev;  
        prev = node;  
        node = next;  
    }  
    return prev;  
}
```
# 🧠 Ideas about Problem

# 🔗 Related Applications


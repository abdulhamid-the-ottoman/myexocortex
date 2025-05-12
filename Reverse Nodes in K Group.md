---
created:
  - 2023-07-01 18:45
share: true
---

up::

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return _the modified list_.
> 
> `k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.
> 
> You may not alter the values in the list's nodes, only nodes themselves may be changed.
> 
> ![Pasted image 20230701184553.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230701184553.png)
> 
> **Constraints:**
> 
> - The number of nodes in the list is `n`.
> - `1 <= k <= n <= 5000`
> - `0 <= Node.val <= 1000`
> 
> **Follow-up:** Can you solve the problem in `O(1)` extra memory space?

## 🔑 **Key Points of Understanding**
- Here is the needs to be done pictorially:
![Pasted image 20230702191712.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230702191712.png)


# 🔍 Solutions
- we will reverse the groups of k elements at once. we can do that as follows.
```C++
ListNode *reverse(ListNode * prev,ListNode *current, int k) {  
    if(k == 0){  
        return prev;  
    }  
    else{  
        ListNode * node = reverse(current, current->next, --k);  
        node->next = prev;  
        return prev;  
    }  
}
```

- We as you may see that we have to be linking the last of each group. 
	- We can do this by advancing on the linked list.
	 ```C++
	ListNode* advance(ListNode* node, int step){  
	    ListNode* prev = nullptr;  
	    for(int i= 0; i < step && node != nullptr; ++i ){  
	        prev = node;  
	        node = node->next;  
	    }  
	    if(!node){  
	        return prev;  
	    }  
	    return node;  
	}
	```
	- We can determine what to link by advancing from the head.
	
	- We can determine the next group by advancing from the head as well.

```C++
ListNode *reverseKGroup(ListNode *head, int k) {  
    ListNode * current = head;  
    /*first advance gives us the head of the new linked list*/  
    ListNode * retlist = advance(current,k-1);  
    while(current->next!= nullptr){  
        /*we have to calculate the next block the reverse*/  
        ListNode* next_block = advance(current,k);  
        /*we calculate where to link after reversal*/  
        ListNode* next_link  = advance(current,2*k-1);  
        /*reverse the current block and link*/  
        reverse(next_link,current,k);  
        /*iterate to the next block*/  
        current = next_block;  
    }  
    return retlist;  
}
```

# 🧠 Ideas about Problem

# 🔗 Related Applications


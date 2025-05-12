---
created:
  - 2023-07-03 10:48
share: true
---

up::[Trees](NeetCode%20Index.md#^de270e)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.
> 
> Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.
> 
> ![Pasted image 20230703104953.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230703104953.png)
> 
> **Constraints:**
> 
> - The number of nodes in both trees is in the range `[0, 100]`.
> - `-104 <= Node.val <= 104`

## 🔑 **Key Points of Understanding**
- We can solve this problem by doing a pre-order traversal
	- checking whether 2 nodes are the same
	- checking the left tree is the same
	- checking the right tree is the same.

# 🔍 Solutions
```C++
class Solution {  
public:  
    bool isSameTree(TreeNode* p, TreeNode* q) {  
        if(!p && !q ){  
            return true;  
        }else if((!p && q) || (!q&&p)){  
            return false;  
        }else{  
            return p->val == q->val && isSameTree(p->left,q->left) && isSameTree(p->right,q->right);  
        }  
    }  
};
```
# 🧠 Ideas about Problem

# 🔗 Related Applications


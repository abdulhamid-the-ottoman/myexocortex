---
created:
  - 2023-07-06 15:56
share: true
---

up::[Trees](NeetCode%20Index.md#^27a48d)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Given the `root` of a binary search tree, and an integer `k`, return _the_ `kth` _smallest value (**1-indexed**) of all the values of the nodes in the tree_.
> 
> ![400](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230706155725.png)
> 
> **Constraints:**
> 
> - The number of nodes in the tree is `n`.
> - `1 <= k <= n <= 104`
> - `0 <= Node.val <= 104`
> 
> **Follow up:** If the BST is modified often (i.e., we can do insert and delete operations) and you need to find the kth smallest frequently, how would you optimize?



## 🔑 **Key Points of Understanding**
- $1^{st}$ way: you can in order traverse the whole tree into a vector and select the k-1 th element
- $2^{nd}$ way: you can in order traverse the array and decrease k at current node using a pointer and capture the result when k is zero
# 🔍 Solutions
```C++
class Solution {  
private:  
    void inorder(TreeNode* root,int* k,int * val){  
        if(!root){  
            return ;  
        }else{  
            inorder(root->left,k,val);  
            if(--(*k) == 0){  
                *val= root->val;  
            }  
            inorder(root->right,k,val);  
        }  
    }  
  
public:  
    int kthSmallest(TreeNode* root, int k) {  
        int val = -1;  
        inorder(root,&k,&val);  
        return val;  
    }  
};
```

# 🧠 Ideas about Problem

# 🔗 Related Applications


---
created:
  - 2023-07-06 15:51
share: true
---

up::[ Trees](NeetCode%20Index.md#^27a48d)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Given the `root` of a binary tree, _determine if it is a valid binary search tree (BST)_.
> 
> A **valid BST** is defined as follows:
> 
> - The left subtree of a node contains only nodes with keys **less than** the node's key.
> - The right subtree of a node contains only nodes with keys **greater than** the node's key.
> - Both the left and right subtrees must also be binary search trees.
> 
> ![500](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230706155251.png)
> 
> **Constraints:**
> 
> - The number of nodes in the tree is in the range `[1, 104]`.
> - `-231 <= Node.val <= 231 - 1`



## 🔑 **Key Points of Understanding**
- The key idea is to traverse in a pre-order fashion
	- first you check the current node against its left and right children whether it holds the the criteria
	- Then you do it for left sub-tree and right- sub tree.
# 🔍 Solutions

```C++
class Solution {  
public:  
    bool isValidBST(TreeNode* root) {  
        if(!root){  
            return true;  
        }else{  
            bool result = true;  
            if(root->left){  
                int val = root->left->val;  
                result &= val < root->val;  
            }  
  
            if(root->right){  
                int val = root->right->val;  
                result &= val > root->val;  
            }  
  
            return result && isValidBST(root->left) && isValidBST(root->right);  
  
        }  
    }  
};
```

# 🧠 Ideas about Problem

# 🔗 Related Applications


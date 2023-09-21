---
created: ["2023-07-03 10:55"]
share: true
---

up::

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Given the roots of two binary trees `root` and `subRoot`, return `true` if there is a subtree of `root` with the same structure and node values of `subRoot` and `false`otherwise.
> 
> A subtree of a binary tree `tree` is a tree that consists of a node in `tree` and all of this node's descendants. The tree `tree` could also be considered as a subtree of itself.
> 
> ![Pasted image 20230703105722.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230703105722.png)
> 
> **Constraints:**
> 
> - The number of nodes in the `root` tree is in the range `[1, 2000]`.
> - The number of nodes in the `subRoot` tree is in the range `[1, 1000]`.
> - `-104 <= root.val <= 104`
> 
> - `-104 <= subRoot.val <= 104`


## 🔑 **Key Points of Understanding**
- We can check equality at every node, if they are not the same, we check with left and right subtree.
# 🔍 Solutions
```C++
class Solution {  
private:  
    bool isSame(TreeNode * r1, TreeNode* r2){  
        if(!r1 && !r2){  
            return true;  
        }  
        else if((!r1 && r2) || (!r2 && r1)){  
            return false;  
        }  
        else{  
            return r1->val == r2->val && isSame(r1->left,r2->left) && isSame(r1->right,r2->right);  
        }  
    }  
public:  
    bool isSubtree(TreeNode* root, TreeNode* subRoot) {  
        if(!root && !subRoot){  
            return true;  
        }  
        else if(!root && subRoot){  
            return false;  
        }  
        else if(isSame(root,subRoot)){  
            return true;  
        }else{  
            return isSubtree(root->left,subRoot) || isSubtree(root->right,subRoot);  
        }  
    }  
};
```
# 🧠 Ideas about Problem

# 🔗 Related Applications


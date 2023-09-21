---
created: ["2023-07-08 11:23"]
share: true
---

up::[Trees](NeetCode%20Index.md#^27a48d)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> - A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.
> 
> - The **path sum** of a path is the sum of the node's values in the path.
> 
> - Given the `root` of a binary tree, return _the maximum **path sum** of any **non-empty** path_.
> 
> ![500](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230708112655.png)
> 
> **Constraints:**
> 
> - The number of nodes in the tree is in the range `[1, 3 * 104]`.
> - `-1000 <= Node.val <= 1000`

## 🔑 **Key Points of Understanding**
- This has to be post-order traversal : 
	- \<left sub tree\> \<right sub tree\> \<root\>
- update the max variable recursively
# 🔍 Solutions
```C++
class Solution {  
private:  
    int maxPath(TreeNode* root, int* maxval){  
        if(!root){  
            return 0;  
        }  
        else{  
            int val =  root->val + maxPath(root->left,maxval) + maxPath(root->right,maxval);  
            if(*maxval < val){  
                *maxval = val;  
            }  
            return val;  
        }  
    }  
public:  
    int maxPathSum(TreeNode* root) {  
        int max = 0;  
        maxPath(root,&max);  
        return max;  
    }  
};
```
# 🧠 Ideas about Problem

# 🔗 Related Applications


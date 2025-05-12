---
created:
  - 2023-07-03 11:39
share: true
---

up::[Trees](NeetCode%20Index.md#^de270e)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST.
> 
> According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”
> 
> ![Pasted image 20230703114154.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230703114154.png)
> 
> **Constraints:**
> 
> - The number of nodes in the tree is in the range `[2, 105]`.
> - `-109 <= Node.val <= 109`
> - All `Node.val` are **unique**.
> - `p != q`
> - `p` and `q` will exist in the BST.


## 🔑 **Key Points of Understanding**
- we are looking for a node which is between the min and max given as 2 tree nodes. 
	- Because this is the case there happens a fork in the road.
- If root's val is smaller than the min, we direct the search to the right.
- If root's val is greater than the max, we direct the search to the left.
# 🔍 Solutions
```C++
class Solution {  
public:  
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {  
        int pval = p->val;  
        int qval = q->val;  
        int rval = root->val;  
  
        int min = pval > qval ? qval : pval;  
        int max = pval > qval ? pval : qval;  
  
        if(rval < min){  
            return lowestCommonAncestor(root->right,p,q);  
        }  
        else if(rval > max){  
            return lowestCommonAncestor(root->left,p,q);  
        }else{  
            return root;  
        }  
    }  
};
```
# 🧠 Ideas about Problem

# 🔗 Related Applications


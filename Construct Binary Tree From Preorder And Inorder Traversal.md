---
created: ["2023-07-06 17:40"]
share: true
---

up::[Trees](NeetCode%20Index.md#^27a48d)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
>Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return _the binary tree_.
> 
> ![400](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230706174116.png)
> 
> **Constraints:**
> 
> - `1 <= preorder.length <= 3000`
> - `inorder.length == preorder.length`
> - `-3000 <= preorder[i], inorder[i] <= 3000`
> - `preorder` and `inorder` consist of **unique** values.
> - Each value of `inorder` also appears in `preorder`.
> - `preorder` is **guaranteed** to be the preorder traversal of the tree.
> - `inorder` is **guaranteed** to be the inorder traversal of the tree.

## 🔑 **Key Points of Understanding**
- [3,9,20,15,7] => PreOrder
- [9,3,15,20,7] => InOrder

- First element of the pre-order list gives us the root the remainder gives us left sub-tree and right sub-tree
- In order traversal is partitioned as \<left-sub-tree\> , root and \<right-sub-tree\>
- once we get the root, we can search for it in the inorder list and figure out the left and right sub trees and their lengths, their lengths will be the same in preorder traversal.
- So once again we have 2 of the same problem with left sub tree and right subtree, we will solve them recursively and link the left and right pointers of the root.
# 🔍 Solutions
```C++
TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {  
    /*root from the preorder*/  
    TreeNode* root = getRoot(preorder);  
    /*left subtree inorder*/  
    vector<int> lsti = getLSTI(inorder,root->val);  
    /*left subtree preorder*/  
    vector<int> lstp = getLSTP(preorder,lsti.size());  
    root.left = buildTree(lsti,lstp);  
    /*right subtree inorder*/  
    vector<int> rsti = getRSTI(inorder,root->val);  
    /*right subtree preorder*/  
    vector<int> rstp = getRSTP(preorder,lsti.size());  
    /*link them*/  
    root.right = buildTree(rsti,rstp);  
    return root;  
}
```

# 🧠 Ideas about Problem

# 🔗 Related Applications


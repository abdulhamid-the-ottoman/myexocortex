---
created:
  - 2023-07-02 19:30
share: true
---

up:: [Trees](NeetCode%20Index.md#^de270e)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Contents

Given the `root` of a binary tree, invert the tree, and return _its root_.
![Pasted image 20230702193217.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230702193217.png)
**Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

## 🔑 **Key Points of Understanding**
- you need to invert the left tree
- you need to invert the right tree
- and swap left and right of the current node.
# 🔍 Solutions
```C++
  
class Solution {  
public:  
    TreeNode* invertTree(TreeNode* root) {  
        if(root== nullptr || isLeaf(root)){  
            return root;  
        }  
        else{  
            TreeNode* left = invertTree(root->left);  
            TreeNode* right = invertTree(root->right);  
            root->left = right;  
            root->right = left;  
            return root;  
        }  
    }  
private:  
    bool isLeaf(TreeNode * node){  
        return (node->left == nullptr) && (node->right == nullptr);  
    }  
};
```
# 🧠 Ideas about Problem

# 🔗 Related Applications


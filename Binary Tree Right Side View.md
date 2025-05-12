---
created:
  - 2023-07-06 15:36
share: true
---

up::[Trees](NeetCode%20Index.md#^27a48d)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> - Given the `root` of a binary tree, imagine yourself standing on the **right side** of it, return _the values of the nodes you can see ordered from top to bottom_.
> ![400](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230706153819.png)
> 
> **Example 2:**
> 
> **Input:** root = [1,null,3]
> **Output:** [1,3]
> 
> **Example 3:**
> 
> **Input:** root = []
> **Output:** []
> 
> **Constraints:**
> 
> - The number of nodes in the tree is in the range `[0, 100]`.
> - `-100 <= Node.val <= 100`

## 🔑 **Key Points of Understanding**
- Visit the node, and push the element to a vector
	- visit the right node next until it becomes `null`, meaning no more to visit.

# 🔍 Solutions
```C++
class Solution {  
private:  
    void traverse_right(TreeNode* node, vector<int>& traversed){  
        if(!node){  
            return;  
        }else{  
            traversed.push_back(node->val);  
            traverse_right(node->right, traversed);  
        }  
    }  
public:  
    vector<int> rightSideView(TreeNode* root) {  
        vector<int> result;  
        traverse_right(root,result);  
        return result;  
    }  
};
```
# 🧠 Ideas about Problem

# 🔗 Related Applications


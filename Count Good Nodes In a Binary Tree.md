---
created: ["2023-07-06 15:42"]
share: true
---

up::[ Trees](NeetCode%20Index.md#^27a48d)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Given a binary tree `root`, a node _X_ in the tree is named **good** if in the path from root to _X_ there are no nodes with a value _greater than_ X.
> 
> Return the number of **good** nodes in the binary tree.
> 
> ![Pasted image 20230706154420.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230706154420.png)
> 
> **Constraints:**
> 
> - The number of nodes in the binary tree is in the range `[1, 10^5]`.
> - Each node's value is between `[-10^4, 10^4]`.

## 🔑 **Key Points of Understanding**
- You traverse the tree in pre-order form. (top-down)
	- checking whether the current node is bigger or equal to the max element encountered on the path so far. if so we add 1, otherwise 0

# 🔍 Solutions
```C++
class Solution {  
private:  
    int max2(int v1,int v2){  
        return v1 > v2 ? v1 : v2;  
    }  
    int traverse(TreeNode* node, int max){  
        if(!node){  
            return 0;  
        }  
        else{  
            int addend = node->val >= max ? 1 : 0;  
            int maxval = max2(node->val, max);  
            return addend + traverse(node->left,maxval) + traverse(node->right,maxval);  
        }  
    }  
public:  
    int goodNodes(TreeNode* root) {  
        return traverse(root,-1);  
    }  
};
```
# 🧠 Ideas about Problem

# 🔗 Related Applications


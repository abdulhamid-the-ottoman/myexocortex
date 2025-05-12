---
created:
  - 2023-07-03 12:25
share: true
---

up::[Trees](NeetCode%20Index.md#^27a48d)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Given the `root` of a binary tree, return _the level order traversal of its nodes' values_. (i.e., from left to right, level by level).
> ![Pasted image 20230703122638.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230703122638.png)
> **Constraints:**
> 
> - The number of nodes in the tree is in the range `[0, 2000]`.
> - `-1000 <= Node.val <= 1000`

## 🔑 **Key Points of Understanding**
- For level order traversal , you need a queue where you fill by going in both left and right pointers.
	- The number of elements at a time gives you the number of elements at that level.
	- So you know how many elements you have at a level to pop.

# 🔍 Solutions

```C++
class Solution {  
public:  
    vector<vector<int>> levelOrder(TreeNode* root) {  
        vector<vector<int>> res;  
        queue<TreeNode*> q;  
        q.push(root);  
  
        while(!q.empty()){  
            int noe = q.size();  
            vector<int> level;  
            for(int i = 0 ; i < noe; ++i){  
                TreeNode* node = q.front();  
                q.pop();  
                if(node){  
                    level.push_back(node->val);  
                    if(node->left){  
                        q.push(node->left);  
                    }  
                    if(node->right){  
                        q.push(node->right);  
                    }  
                }  
            }  
            if(!level.empty()){  
                res.push_back(level);  
            }  
        }  
  
        return res;  
    }  
};
```

# 🧠 Ideas about Problem

# 🔗 Related Applications


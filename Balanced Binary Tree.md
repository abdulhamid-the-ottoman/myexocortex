---
created: ["2023-07-03 10:32"]
share: true
---

up::[ Trees](NeetCode%20Index.md#^de270e)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Given a binary tree, determine if it is **height-balanced**
> ![Pasted image 20230703103437.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230703103437.png)
> **Constraints:**
> 
> - The number of nodes in the tree is in the range `[0, 5000]`.
> - `-104 <= Node.val <= 104`

## 🔑 **Key Points of Understanding**
## In-order traversal
```C++
void inorder(Node* node){
	if(!node){
		return;
	}
	inorder(node->left);
	visit(node);
	inorder(node->right);
}
```
-  Pay attention the output is the form of
	- \<left sub-tree result\> \<node output\> \<right sub-tree result\>
## Pre-order traversal
```C++
void preorder(Node* node){
	if(!node){
		return;
	}
	visit(node);
	preorder(node->left);
	preorder(node->right);
}
```
- Pay attention the output is the form of
	- \<node result\>\<left-sub-tree result\>\<right-sub-tree-result\>

## Post-order traversal
```C++
void postorder(Node* node){
	if(!node){
		return;
	}
	postorder(node->left);
	postorder(node->right);
	visit(node);
}
```
- Pay attention the output is in the form of:
	- \<left-sub-tree result\>\<right-sub-tree result\>\<node result\>

- The idea is the same, we have to check at every node whether left sub-tree and right- subtree height differs more than 1 
	- We do this by doing a post-order traversal and updating a global variable.

# 🔍 Solutions
```C++
class Solution {  
private:  
    bool balanced;  
    int abs(int val){  
        return val > 0 ? val : -val;  
    }  
  
    int max2(int v1, int v2){  
        return v1 > v2 ? v1 : v2;  
    }  
    int height(TreeNode* node){  
        if(!node){  
            return -1;  
        }  
        else{  
            int left = height(node->left);  
            int right = height(node->right);  
            balanced &= abs(left-right) <= 1;  
            return 1+ max2(left,right);  
        }  
    }  
public:  
    Solution():balanced(true){  
  
    }  
  
    bool isBalanced(TreeNode* root) {  
        height(root);  
        return balanced;  
    }  
};
```
# 🧠 Ideas about Problem

# 🔗 Related Applications


---
created: ["2023-07-02 19:53"]
share: true
---

up::[ Trees](NeetCode%20Index.md#^de270e)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Given the `root` of a binary tree, return _the length of the **diameter** of the tree_.
> 
> The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the `root`.
> 
> The **length** of a path between two nodes is represented by the number of edges between them.
> 
> ![Pasted image 20230702195539.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230702195539.png)
> 
> **Constraints:**
> 
> - The number of nodes in the tree is in the range `[1, 104]`.
> - `-100 <= Node.val <= 100`

## 🔑 **Key Points of Understanding**
- The height of a null tree is -1.
- The longest path running through a particular node is calculated as depth of the left - subtree + depth of the right sub-tree + 2
- We calculate the depth of the tree as 1+ max(depth(left),depth(right))
- We have to keep the max length in a global variable
# 🔍 Solutions

# 🧠 Ideas about Problem

# 🔗 Related Applications


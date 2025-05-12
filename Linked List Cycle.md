---
created:
  - 2023-06-30 16:39
share: true
---

up::[ Linked List](NeetCode%20Index.md#^f40e13)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> - Given `head`, the head of a linked list, determine if the linked list has a cycle in it.
> - There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to. **Note that `pos` is not passed as a parameter**.
> - Return `true` _if there is a cycle in the linked list_. Otherwise, return `false`.
> - Examples:
>  ![Pasted image 20230630164136.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230630164136.png)
>  
> **Constraints:**
> 
> - The number of the nodes in the list is in the range `[0, 104]`.
> - `-105 <= Node.val <= 105`
> - `pos` is `-1` or a **valid index** in the linked-list.
> 
> **Follow up:** Can you solve it using `O(1)` (i.e. constant) memory?


## 🔑 **Key Points of Understanding**
- You can augment the nodes with visited boolean, and  start traversing the linked list and see whether you reach a visited = true node.
	- This takes O(n) memory
- You can also walk with 2 pointers, 
	- you can walk with one pointer at the speed of 1 node.
	- you can walk with the other pointer at the speed of 2 node.
	- Once they meet each other you can take the slow running to the beginning of the list and let them run together.
	- Their next meeting is the start of the loop!

# 🔍 Solutions

# 🧠 Ideas about Problem

# 🔗 Related Applications


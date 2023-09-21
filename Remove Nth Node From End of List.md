---
created: ["2023-06-30 18:39"]
share: true
---

up::[ Linked List](NeetCode%20Index.md#^f40e13)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.
> 
> ![Pasted image 20230630184303.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230630184303.png)
> **Constraints:**
> 
> - The number of nodes in the list is `sz`.
> - `1 <= sz <= 30`
> - `0 <= Node.val <= 100`
> - `1 <= n <= sz`
> 
> **Follow up:** Could you do this in one pass?

## 🔑 **Key Points of Understanding**

- [1 2 3 4 5]  n = 2
	- we can do this by keeping 2 pointers which has a constant distance of 2 
	- L:1 R:3, we keep moving them both until R reaches to the NULL
	- L:2 R:4
	- L:3 R:5
	- L:4 R:NULL , now L points to 4.
 
# 🔍 Solutions

# 🧠 Ideas about Problem

# 🔗 Related Applications


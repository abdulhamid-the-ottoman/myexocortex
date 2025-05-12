---
created:
  - 2023-07-01 13:02
share: true
---

up::[ Linked List](NeetCode%20Index.md#^f40e13)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> -You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.
> 
> -You may assume the two numbers do not contain any leading zero, except the number 0 itself.
> 
> ![Pasted image 20230701130506.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230701130506.png)
> 
> **Constraints:**
> 
> - The number of nodes in each linked list is in the range `[1, 100]`.
> - `0 <= Node.val <= 9`
> - It is guaranteed that the list represents a number that does not have leading zeros.


## 🔑 **Key Points of Understanding**
- Simple problem:
	- Walk the both list at the same time,
	- sum the corresponding elements
		- if sum > 10 , then your carry is 1 else 0.
	- if one of the list terminates early, we go with the next as the element is being 0.

# 🔍 Solutions

# 🧠 Ideas about Problem

# 🔗 Related Applications


---
created: ["2023-06-30 17:48"]
share: true
---

up::[Linked List](NeetCode%20Index.md#^f40e13)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> - You are given the head of a singly linked-list. The list can be represented as:
> 
> L0 → L1 → … → Ln - 1 → Ln
> 
> -Reorder the list to be on the following form:
> 
> L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
> 
> You may not modify the values in the list's nodes. Only nodes themselves may be changed.
> ![Pasted image 20230630175645.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230630175645.png)
> **Constraints:**
> 
> - The number of nodes in the list is in the range `[1, 5 * 104]`.
> - `1 <= Node.val <= 1000`


## 🔑 **Key Points of Understanding**
- Go to the middle of the list. and point left-going(L) and right-going(R) pointers
	- if there are even elements one on the left one on the right side
	- always insertbefore 
	- if L and R different, insertbefore,
		- else move to right and insert before

- [1 2 3 4 5] -> L : 3 R:3
	- move to right R:4 --> insert before [4-3]
	- move to left L:2 --> insert before  [2-4-3]
	- move to right R:5 --> insert before [5-2-4-3]
	- move to left L:1 --> insert before [1-5-2-4-3]
- [1 2 3 4] -> L:2 R:3
	- insert before --> [2-3]
	- move to right R:4 --> insert before [4-2-3]
	- move to left L :1 -> insert before [1-4-2-3]
# 🔍 Solutions

# 🧠 Ideas about Problem

# 🔗 Related Applications


---
created:
  - 2023-06-30 19:01
share: true
---

up::[ Linked List](NeetCode%20Index.md#^f40e13)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> A linked list of length `n` is given such that each node contains an additional random pointer, which could point to any node in the list, or `null`.
> 
> Construct a [**deep copy**](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) of the list. The deep copy should consist of exactly `n` **brand new** nodes, where each new node has its value set to the value of its corresponding original node. Both the `next` and `random` pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. **None of the pointers in the new list should point to nodes in the original list**.
> 
> For example, if there are two nodes `X` and `Y` in the original list, where `X.random --> Y`, then for the corresponding two nodes `x`and `y` in the copied list, `x.random --> y`.
> 
> Return _the head of the copied linked list_.
> 
> The linked list is represented in the input/output as a list of `n` nodes. Each node is represented as a pair of `[val, random_index]`where:
> 
> - `val`: an integer representing `Node.val`
> - `random_index`: the index of the node (range from `0` to `n-1`) that the `random` pointer points to, or `null` if it does not point to any node.
> 
> Your code will **only** be given the `head` of the original linked list.
>
> ![Pasted image 20230630190432.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230630190432.png)
> 
> **Constraints:**
> 
> - `0 <= n <= 1000`
> - `-104 <= Node.val <= 104`
> - `Node.random` is `null` or is pointing to some node in the linked list.

## 🔑 **Key Points of Understanding**
- On first walk of the linked list with next pointers.
	- We will create a hash-map where the keys of the hash-map is the value of node elements and the value of the hash-map is the nodes themselves
- On the second walk, we will check every random pointer.
	- We will update the random pointers by checking the value using the hashmap and link the random pointer to the value of the hash-map.

# 🔍 Solutions

# 🧠 Ideas about Problem

# 🔗 Related Applications


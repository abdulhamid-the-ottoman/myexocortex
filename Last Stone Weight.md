---
created:
  - 2023-07-09 22:00
share: true
---

up::[Heaps](NeetCode%20Index.md#^c810f8)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> You are given an array of integers `stones` where `stones[i]` is the weight of the `ith` stone.
> 
> We are playing a game with the stones. On each turn, we choose the **heaviest two stones** and smash them together. Suppose the heaviest two stones have weights `x`and `y` with `x <= y`. The result of this smash is:
> 
> - If `x == y`, both stones are destroyed, and
> - If `x != y`, the stone of weight `x` is destroyed, and the stone of weight `y` has new weight `y - x`.
> 
> At the end of the game, there is **at most one** stone left.
> 
> Return _the weight of the last remaining stone_. If there are no stones left, return `0`.
> 
> ![Pasted image 20230709220113.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230709220113.png)
> 
> **Constraints:**
> 
> - `1 <= stones.length <= 30`
> - `1 <= stones[i] <= 1000`


## 🔑 **Key Points of Understanding**
- while (there is more than 1 element):
	- create a heap and pop it twice
		- if x != y:
			- push_back(y-x)

# 🔍 Solutions

# 🧠 Ideas about Problem

# 🔗 Related Applications


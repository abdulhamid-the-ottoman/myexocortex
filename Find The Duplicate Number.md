---
created:
  - 2023-07-01 13:41
share: true
---

up::

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> - Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.
> 
> - There is only **one repeated number** in `nums`, return _this repeated number_.
> 
> - You must solve the problem **without** modifying the array `nums` and uses only constant extra O(1) space.
> 
> **Example 1:**
> 
> **Input:** nums = [1,3,4,2,2]
> **Output:** 2
> 
> **Example 2:**
> 
> **Input:** nums = [3,1,3,4,2]
> **Output:** 3
> 
> **Constraints:**
> 
> - `1 <= n <= 105`
> - `nums.length == n + 1`
> - `1 <= nums[i] <= n`
> - All the integers in `nums` appear only **once** except for **precisely one integer** which appears **two or more**times.
> 
> **Follow up:**
> 
> - How can we prove that at least one duplicate number must exist in `nums`?
> - Can you solve the problem in linear runtime complexity?

## 🔑 **Key Points of Understanding**
- This is classic tortoise and hare (Floyd) algorithm. So let's first explain
## The Floyd's Algorithm
- In a linked list, we can detect a cycle using this algorithm
	- We have a slow pointer represented by a red dot.
	- We have a fast pointer represented by a green dot.
![Pasted image 20230701142458.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230701142458.png)
![Pasted image 20230701142528.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230701142528.png)

- We know that fast and slow pointer will meet at a node in the circle as shown below.
![Pasted image 20230701143022.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230701143022.png)
- When this happens, we take one of the pointers and put it at the start of the list and start stepping one node at a time (both go one step at a time- this is important)
	- next time they meet, they meet at the start of the cycle.

![Pasted image 20230701143410.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230701143410.png)

- Now back to the question. We have the the array as follows, 

| 0   | 1   | 2   | 3   | 4   |
| --- | --- | --- | --- | --- |
| 3   | 1   | 3   | 4   | 2   | 

- The linked list representation:
0 -> 3 -> 4 -> 2 -> 3

- our slow and fast pointers
![Pasted image 20230701144809.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230701144809.png)
- They meet at node 2 at first and then
	- we find the start of the loop at node 3.
	- This is also the duplicate!


# 🔍 Solutions

# 🧠 Ideas about Problem
- Why this algorithm works in this particular example.
	- First of all every duplicate gives a cycle.
	- Since we have only one duplicate we have 1 cycle.
 - And the numbers are in 1-n where our arrays indices run between 0 and n with one duplicate value. 
	 - This helps us knowing that it can be represented as a linked list with one cycle.
- Now why does the Floyd's Algorithm work?
	- This linked list is composed of 3 parts
![Pasted image 20230701150219.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230701150219.png)
- Red part, the length of the linked list until the start of the cycle - x
- Purple part, the length of the list between start and before where slow and fast pointer meets - y
- Orange part, the length of the list between meeting point until the start of the cycle - z
- the length of the cycle l = z+y
- fast pointer travels the distance f = x + $c_1$l + y , fast pointer can traverse the cycle $c_1$ times
- slow pointer travels the distnace s= x+ $c_2$l + y, slow pointer can traverse the cycle $c_2$ times.
- We know that fast is traveling 2 times faster than slow pointer. meaning 2s = f
	- 2(x+$c_2$l + y) = x + $c_1$l + y, if we simplify the equation
	- x+y = ($c_1$ - 2$c_2$)l, and we pull x
	- x = ($c_1$ - 2$c_2$)l - y. 
		- This means the distance before the cycle is equal to certain amount of loops minus the distance before the meeting point.
		- we can rewrite it as follows:
	- x = ($c_1$ - 2$c_2$ -1 ) l + l-y
		- x = $c_3$ l + l-y (l = z+y)
		- x = $c_3$l + z+y - y
		- x = $c_3$l + z
			- this tells us that the distance before the cycle is equal to certain amount of cycle plus the distance after meeting point.
- if we take $c_3$ = 0 , then it is obvious that x =z that's why when a pointer from the head and the where they meet travels, they will meet at the start of the cycle.
# 🔗 Related Applications


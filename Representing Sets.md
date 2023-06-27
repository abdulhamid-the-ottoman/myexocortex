---
share: true
---

up:: [Symbolic Data](./SICP.md#^369430)
tags:: #set_representation

# Representing Sets
- There are a number of possible ways we could represent sets.
- A set is a collection of distinct objects.
- Our sets need to work with the following operations:

|Procedure|Result|
|---|---|
|`(element-of-set? x s)`|Is `x` a member of the set `s`?|
|`(adjoin-set x s)`|Set containing `x` and the elements of set `s`|
|`(union-set s t)`|Set of elements that occur in either `s` or `t`|
|`(intersection-set s t)`|Set of elements that occur in both `s` and `t`|

## Set as unordered lists

^b7989b

- One method is to just use lists. 
	- Each time we add a new element, we have to check to make sure it isn't already in the set.
	- This isn't very efficient.
		- `element-of-set?` and `adjoin-set` are $\Theta$(n)
			- we have to walk all the elements in the list
		- `union-set` and `intersection-set`  are $\Theta$($n^2$)
			- we have to compare every element in the second set for each element of the first set.
		- We can make `adjoin-set` $\Theta$(1) if we allow duplicates, but then the list would grow very large, which still can cause decrease in performance

## Sets as ordered lists

^b15ab6

- A more efficient representation is a ordered list
- To keep things simple, we will only consider sets of numbers
- Now, scanning the entire list in `element-of-set?` is a worst-case scenario.
	- On the average, we should expect to scan half of the list.
- This is still $\Theta$(n), but now we can make `union-set` and `intersection-set` $\Theta$(n)


## Sets as binary trees

^02d5fc

- An even more efficient representation is a binary tree where left branches contain smaller numbers and right branches contain larger numbers.
- The same set can be represented by such a tree in many ways
- If the tree is balanced, each subtree is about half the size of the original tree.
	- This allows us to implement `element-of-set?` in $\Theta$(log(n)) time.
- We will represent each node by `(list number left-subtree right-subtree)`
- Efficiency hinges on the tree being balanced. 
	- We can write a procedure to balance trees, or we could use a different data structure (B-trees or red-black trees)

## Sets and information retrieval

^5ac1be

- The techniques discussed for sets show up again and again in information retrieval
- In data management system, each record is identified by a unique key.
- The simplest, least efficient method is to use an unordered list with $\Theta$(n) access.
- For fast "random access", trees are usually used.
- Using data abstraction, we can start with unordered lists and then later change the constructors and selectors to use a tree representation.
---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [Set as unordered lists](Representing%20Sets.md#^b7989b)
	- [ Exercise 59](SICPE%202.59.md)
	- [ Exercise 60](SICPE%202.60.md)
- [Sets as ordered lists](Representing%20Sets.md#^b15ab6)
	- [Exercise 61](SICPE%202.61.md)
	- [ Exercise 62](SICPE%202.62.md)
- [ Sets as binary trees](Representing%20Sets.md#^02d5fc)
	- [ Exercise 63](SICPE%202.63.md)
	- [ Exercise 64](SICPE%202.64.md)
	-  [ Exercise 65](SICPE%202.65.md)
- [ Sets and information retrieval](Representing%20Sets.md#^5ac1be%20)
	- [ Exercise 66](SICPE%202.66.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
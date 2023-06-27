---
share: true
---

up:: [Building Abstractions with Data](./SICP.md#^d1c4f8)
tags:: #hierarchical_data #closure_property

# Hierarchical Data and the Closure Property
- Pairs form a primitive "glue" for compound data objects
- We can visualize pairs with *box and pointer* notation. 
	- Each pair is a double box, and both sides have an arrow pointing to a primitive data object, or to another pair.
- The closure property of `cons` is the ability to make pairs whose elements are pairs.
	- This allows us to create hierarchical structures.
- We have been using closure all along with combinations. Now, we are going to use closure for compound data.

> [!INFO]  Representing Compound Data
> - The use of the word "closure" here comes from abstract algebra, where a set of elements is said to be closed under an operation if applying the operation to elements in the set produces an element that is again an element of the set.
> - The Lisp community also (unfortunately) uses the word "closure" to describe a totally unrelated concept:
> 	- A closure is an implementation technique for representing procedures with free variables.
> 	- We don't use the word "closure" as the Lisp Community does!
---

---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- 
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
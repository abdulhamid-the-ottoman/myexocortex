---
share: true
---

up:: [ Systems with Generic Operations](./SICP.md#^daebf9)
tags:: 

# Combining Data of Different Types
- In our unified arithmetic system, we ignored an important issue:
	- We didn't consider operations that cross type boundaries.
	- Ex: a Scheme number and rational number addition.
- One solution would be to design a procedure for every possible combination of types.
	- This is cumbersome and it violates the modularity.

## Coercion
- Often the different data types are not completely independent.
- For example, any real number can be expressed as a complex number with an imaginary part of zero.
- We can make all operations work on combinations of Scheme numbers and complex numbers by coercing former to the latter.
- Here is a typical coercion procedure:

```Scheme
(define (scheme-number->complex n) 
  (make-complex-from-real-imag (contents n) 0))
```

- The big advantage of coercion is that, although we may need to write many coercion procedures,
	- we only need to implement each operation once per type.
- We could modify `apply-generic` to try coercion if there is no specific procedure available for the given types.
- But it gets complicated. 
	- What if both types can be converted to a third type?
	- What if multiple coercions are required?
	- We end up with a graph of relations among types.

## Hierarchies of types
- We can simplify the problem by using a type hierarchy instead of an arbitrary graph.
- In the hierarchy, each type is related to super-types above it and subtypes below it.
- A *tower* is a hierarchy where each type has at most one super-type and sub-type.
- Our numeric tower comprises integers, rationals, real numbers and complex numbers.
- Coercion then simply becomes a matter of raising the argument whose type is lower in the tower to the level of the other type.
- We can write fewer procedures by allowing types to *inherit their super-type's* operations.
- In some cases, we can *simplify* results by lowering a value down the type tower.


## Inadequacies of hierarchies

^c9f254

- In general, a type may have more than one sub-type. This is easy to deal with.
- Allowing multiple super types (known as *multiple inheritance*) is tricky, since the type can be raised via multiple paths to search for a procedure.
- Having large numbers of inter-related types conflict with modularity.

> [!INFO]  Representing Compound Data
>  - Developing a useful, general framework for expressing the relations among different types of entities ( what philosophers call *ontology*) seems intractably difficult.
>  - The main difference between the confusion that existed ten years ago and the confusion that exists now is that now a variety of inadequate ontological theories have been embodied in a plethora of correspondingly inadequate programming languages.
> 	 - Much of the complexity of OOP languages - and the subtle and confusing differences among contemporary OOP languages - centers on the treatment of generic operations on inter-related types.

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [ Inadequacies of hierarchies](Combining%20Data%20of%20Different%20Types.md#^c9f254)
	- [ Exercise 81 ](SICPE%202.81.md)
	- [ Exercise 82 ](SICPE%202.82.md)
	- [ Exercise 83 ](SICPE%202.83.md)
	- [ Exercise 84 ](SICPE%202.84.md)
	- [ Exercise 85 ](SICPE%202.85.md)
	- [ Exercise 86 ](SICPE%202.86.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #evaluating_combinations, #sicp/ch1 

# Evaluating Combinations

- To evaluate a combination:
	 ```Scheme
	 (* (+ 2
           (* 4 6))
        (+ 3 5 7))
```
	1. You have to evaluate the subexpressions of the combination.
		- Evaluation is *recursive* in nature - one of its steps is invoking itself with each element inside it.
	2. Apply the procedure (value of the leftmost subexpression, the operator) to the arguments ( values of the subexpressions, the operands)
		 -  The evaluation of a combination can be represented with a tree, where internal nodes represent the operators, and the children represent the operands.  Or the internal nodes as shown below can represent the results.
		![200x200](tree_representation_with_subcombinations.png)
		- "percolate values upward" form of the evaluation rule is an example of a general kind of process known as *tree accumulation*

- *Recursion* is a powerful technique for dealing with hierarchical, tree-like objects.
- To end the recursion, we stipulate the following:
	- Numbers evaluate to themselves
	- Built-in operators evaluate to machine instruction sequences.
	- Names evaluate to values associated with them in the environment.

- The following is  **not a combination:**
 ```Scheme
 (define x 4)
``` 
 - ```define```  doesn't apply to 2 arguments, that is why this is not a combination.
 - Then what is this called?
	 - Exceptions such as these are called *special forms*.
	 - *Special forms* have their own evaluation rule.
---

## 🔑 Key Points
- 
## ❓ Questions
-  What is the role of the environment?
	- It is determining the meaning of symbols in expressions.
- What is the point of special forms?
	- The various kinds of expressions (each with its associated evaluation rule) constitute the syntax of the programming language
## 📦 Resources
- 
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
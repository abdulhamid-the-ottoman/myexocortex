---
share: true
---
up:: [SICP](./SICP.md)
tags:: #building_abstractions_with_procedures #sicp/ch1

# Building Abstractions with Procedures

## Intro Bulletins
- A computational process evolves to manipulate data.
- The evolution of a computational process is controlled by pattern of rules called a **program**
- Well-designed computational systems are **modular.**
- This book uses the Scheme dialect of Lisp
	- Lisp uses a certain kinds of logical expressions called *recursion equations*, as a model of computation.
- Lisp represents procedures as data (homo-iconity)
	- Lisp is an excellent language for writing programs that manipulates other programs as data such as compilers and interpreters.
## Contents
1. [The Elements of Programming](./The%20Elements%20of%20Programming.md) ^869199
	1. [Expressions](./Expressions.md)
	2. [Naming and the Environment](./Naming%20and%20the%20Environment.md)
	3. [Evaluating Combinations](./Evaluating%20Combinations.md)
	4. [Compound Procedures](./Compound%20Procedures.md)
	5. [The Substitution Model for Procedure Application](./The%20Substitution%20Model%20for%20Procedure%20Application.md)
	6. [Conditional Expressions and Predicates](./Conditional%20Expressions%20and%20Predicates.md)
	7. [Square Roots by Newton's Method](./Square%20Roots%20by%20Newton's%20Method.md)
	8. [Procedures as Black-Box Abstractions](./Procedures%20as%20Black-Box%20Abstractions.md)
2. [Procedures and the Processes They Generate](./Procedures%20and%20the%20Processes%20They%20Generate.md) ^ad5850
	1. [Linear Recursion and Iteration](./Linear%20Recursion%20and%20Iteration.md)
	2. [Tree Recursion](./Tree%20Recursion.md)
	3. [Orders of Growth](./Orders%20of%20Growth.md)
	4. [Exponentiation](./Exponentiation.md)
	5. [Greatest Common Divisors](./Greatest%20Common%20Divisors.md)
	6. [Testing for Primality](./Testing%20for%20Primality.md)
3. [Formulating Abstractions with Higher-Order Procedures](./Formulating%20Abstractions%20with%20Higher-Order%20Procedures.md) ^190218
	1. [Procedures as Arguments](./Procedures%20as%20Arguments.md)
	2. [Constructing Procedures Using Lambda](./Constructing%20Procedures%20Using%20Lambda.md)
	3. [Procedures as General Methods](./Procedures%20as%20General%20Methods.md)
	4. [Procedures as Returned Values](./Procedures%20as%20Returned%20Values.md)
---

## 🔑 Key Points
- 
## ❓ Questions
- What is model of computation?
	- A model of computation is a model which describes how an output of a *mathematical function* is computed given an input.
	- A model describes how units of computations, memories and communications are organized.
	- Models of computation can be classified into 3 categories: 
		- SEQUENTIAL MODELS:
			- Finite State Machines
			- Post machines ([Post-Turing Machines](https://en.wikipedia.org/wiki/Post%E2%80%93Turing_machine)  and [Tag system - Wikipedia](https://en.wikipedia.org/wiki/Tag_system))
			- Pushdown automata
			- Register Machines
				- Random-access machines
			- Turing Machines
			- Decision Tree Model
		- FUNCTIONAL MODELS:
			- Abstract Rewriting Systems
			- Combinatory Logic
			- General Recursive Functions *LISP MODEL*
			- Lambda Calculus
		- CONCURRENT MODELS:
			- Actor model
			- Cellular automaton
			- Interaction nets
			- Kahn process networks
			- Logic gates and digital circuits
			- Petri Nets
			- Synchronous Data Flow
- What is a procedure?
	- Lisp descriptions of processes are called procedures.
- What does modular mean?
	-  A modular system is a collection of building blocks that can be configured in different ways, adapting for different customer needs
## 📦 Resources
- 
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 


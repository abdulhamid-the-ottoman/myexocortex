---
share: true
---

up:: 
tags:: 

# Systematic Program Design

- “Good programming” means an approach to the creation of software that relies on 
	- systematic thought, 
	- planning, 
	- understanding from the very beginning, at every stage, and for every step.
- Any reasonably complete program consists of many building blocks
	- We choose to use functions as fundamental building blocks
	-  The key is to discover
		- which functions are needed,
		- how to connect them, 
		-  how to build them from basic ingredients.
- “Systematic program design” refers to a mix of two concepts: 
	- design recipes 
	-  iterative refinement.
## Design Recipes
- Design Recipes apply to both complete programs and individual functions
- We deal with *just two recipes for complete programs:*
	- one for programs with a graphical user interface (GUI) 
	- one for batch programs
- Function-level design recipes share a common *design process*, **headers written in yellow** specifies the *expected outcomes*, sub-items represent the key *activities* :  ^795d68
	1. **From Problem Analysis to Data Definitions**
		- Identify the information that must be represented
		-  How the information is represented in racket
		- Formulate data definitions and illustrate them with examples.
	2. **Signature, Purpose Statement, Header**
		- State what kind of data the desired function consumes and produces.
		- Formulate a concise answer to the question what the function computes.
		- Define a stub that lives up to the signature.
	3. **Functional Examples**
		- Work through concrete examples that illustrate the function’s purpose.
			- makes you have an understanding of what the desired function is expected to compute.
	4. **Function Template**
		- Translate the data definitions into an outline of the function.
	5. **Function Definition**
		- Fill in the gaps in the function template. Exploit the purpose statement and the examples.
	3. **Testing**
		- Articulate the examples as tests and ensure that the function passes all
		- Doing so discovers mistakes.
		- Tests also supplement examples in that they help others read and understand the definition when the need arises—and it will arise for any serious program.

## Iterative Refinement
- Iterative Refinement addresses the issue that problems are complex and multifaceted.
- Getting everything right at once is *nearly impossible.*
	- computer scientists borrow iterative refinement from the physical sciences to tackle this design problem.
- Iterative refinement recommends *stripping away all inessential details at first* and finding a solution for the remaining core problem.
- A refinement step *adds in one of these omitted details and re-solves the expanded problem*, using the existing solution as much as possible.
- A repetition, also called an iteration, of these refinement steps eventually leads to a complete solution.
- we use iterative refinement to *state increasingly complex variants of the same problem* over the course of the first three parts of the book

## Racket and Languages
- Learning to design programs is primarily about the study of principles and the acquisition of transferable skills
- The ideal programming language must support these two goals:
	- principles 
	- the acquisition of transferable skills
- This books tries to do this in different mini programming languages
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
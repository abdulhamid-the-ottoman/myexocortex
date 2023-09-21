---
share: true
---

up:: 
tags:: 



# Book and Its Parts
- The purpose of this book is to introduce readers without prior experience to the *systematic design of programs.*
- In tandem, it presents *a symbolic view of computation*, a method that explains how the application of a program to data works

- [Prologue: How to Program](https://htdp.org/2023-5-12/Book/part_prologue.html) is a quick introduction to plain programming. It explains how to write a simple animation in *SL.
	- The final note therefore explains why plain programming is wrong and how a systematic, gradual approach to program design eliminates the sense of dread that every beginning programmer usually experiences.
- [Fixed-Size Data](https://htdp.org/2023-5-12/Book/part_one.html) explains the *most fundamental concepts of systematic design* using simple examples
	- The central idea is that designers typically have a rough idea of what data the program is supposed to consume and produce.
	- A systematic approach to design must therefore *extract as many hints as possible from the description of the data that flows into and out of a program.*
	- To keep things simple, this part starts with atomic data—numbers, images, and so on—and then gradually introduces new ways of describing data: intervals, enumerations, itemizations, structures, and combinations of these.
- [Beginning Student Language](https://htdp.org/2023-5-12/Book/i1-2.html) describes the teaching language in complete detail:
	- its vocabulary, its grammar (syntax), and its meaning (semantics).
	- Program designers use this model of computation to predict what their creations compute when run or to analyze error diagnostics.
- [Arbitrarily Large Data](https://htdp.org/2023-5-12/Book/part_two.html) extends [Fixed-Size Data](https://htdp.org/2023-5-12/Book/part_one.html) with the means to describe the most interesting and useful forms of data: arbitrarily large compound data.
	- While a programmer may nest the kinds of data from [Fixed-Size Data](https://htdp.org/2023-5-12/Book/part_one.html) to represent information, the nesting is always of a fixed depth and breadth.
	- This part shows how a subtle generalization gets us from there to data of arbitrary size.
	- The focus then switches to the systematic design of programs that process this kind of data.
	
-  [Quote, Unquote](https://htdp.org/2023-5-12/Book/i2-3.html) introduces a concise and powerful notation for writing down large pieces of data: quotation and anti-quotation.

- [Abstraction](https://htdp.org/2023-5-12/Book/part_three.html) acknowledges that many of the functions from [Arbitrarily Large Data](https://htdp.org/2023-5-12/Book/part_two.html)look alike. They can be generalized
	- No programming language should force programmers to create pieces of code that are so similar to each other.
	- Conversely, every good programming language comes with ways to eliminate such similarities
	- Computer scientists call both the step of eliminating similarities and its result abstraction, and they know that abstractions greatly increase a programmer’s productivity.
	- Hence, this part introduces design recipes for creating and using abstractions.

- [Scope and Abstraction](https://htdp.org/2023-5-12/Book/i3-4.html) plays 2 roles:
	- It injects the concept of lexical scope, the idea that a programming language ties every occurrence of a name to a definition that a programmer can find with an inspection of the code.
	- On the other hand, it explains a teach-pack with additional mechanisms for abstraction, including so-called for loops.

- [Intertwined Data](https://htdp.org/2023-5-12/Book/part_four.html) generalizes [Arbitrarily Large Data](https://htdp.org/2023-5-12/Book/part_two.html) and explicitly introduces 
	- the idea of iterative refinement into the catalog of design concepts.

-  [The Nature of Numbers](https://htdp.org/2023-5-12/Book/i4-5.html) explains and illustrates why decimal numbers work in such strange ways in all programming languages. 
	- Every budding programmer ought to know these basic facts.

- [Generative Recursion](https://htdp.org/2023-5-12/Book/part_five.html) adds a new design principle.
	- While structural design and abstraction suffice for most problems that programmers encounter, they occasionally lead to insufficiently “performant” programs.
	- That is, structurally designed programs might need too much time or energy to compute the desired answers.
	- Computer scientists therefore replace structurally designed programs with programs that benefit from ad hoc insights(buna mahsus feraset/anlayis) into the problem domain.

- [The Cost of Computation](https://htdp.org/2023-5-12/Book/i5-6.html) uses examples from [Generative Recursion](https://htdp.org/2023-5-12/Book/part_five.html)to illustrate how computer scientists think about performance.

- [Accumulators](https://htdp.org/2023-5-12/Book/part_six.html) adds one final trick to the toolbox of designers: accumulators. Roughly speaking, an accumulator adds “memory” to a function.
	- The addition of memory greatly improves the performance of structurally designed functions from the first four parts of the book.
	- For the ad hoc programs from [Generative Recursion](https://htdp.org/2023-5-12/Book/part_five.html), accumulators can make the difference between finding an answer and never finding one.
	
- [Epilogue: Moving On](https://htdp.org/2023-5-12/Book/part_epilogue.html) is both an assessment and a look ahead to what’s next.


## Navigation
![Pasted image 20230802131641.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802131641.png)
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
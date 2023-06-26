---
share: true
---
up:: [SICP](./SICP.md)
tags:: #lisp

# Overview and Introduction to Lisp
## Part 1
#### Computer Science
- It is not a science, and it's not really about computers.
- It  is not about computers in the same way, the astronomy isn't about telescopes.
- We often conflate the essence of a field with its tools.
- It is math....

#### Declarative vs Imperative
- Mathematical *declarative statement* (**what-is knowledge**) :  The square root of x is the y such that $y >= 0$  and  $y^2 = x$
- *Imperative instructions* (**how-to knowledge**): approximate the square root of x with the following steps:
	- Make a guess, G
	- Improve the guess by averaging G and x/G
	- Keep improving until the guess is good enough.

#### Processes and Lisp
- The above is an algorithm. More generally, it is a process.
- What is a process? It is like a magical spirit that lives in the computer.
- The process is directed by a *pattern of rules* (magical spell) called a *procedure*.
- We conjure our spirits in a language called Lisp.
- Lisp is easy to learn just as chess is easy to learn.
- Rules stated in minutes, but there are many implications.
- Much more difficult to become a master programmer, it requires
	- understanding all the implications
	- knowing how to approach problems

#### Complexity and Computer Science
> [!INFO] Highlights
> - The real problems come when we try to build very, very large systems
> - Nobody can really hold them in their heads all at once.
> - The only reason that it is possible is because there are techniques for controlling the complexity of these large systems
> - And these techniques that are controlling complexity are what this course is really about.
>  - And in some sense, that's really what computer science is about.

- Computer scientists are in the *business of controlling complexity*
- This is different from the complexity that others, for example aeronautical engineers deal with, because the complexity in CS in a sense is not real.
- Computer science deals with *idealized components*
- We know as much as we want about the components; no worrying about tolerance.
- Not much difference between *what i can build* and *what i can imagine*
- Other disciplines have physical constraints; in CS, the only constraint is your mind.

> [!INFO] Highlights
> - Computer science is like an abstract form of engineering.
> - It is the kind of engineering where you ignore the constraints that are imposed by reality.

#### Techniques for managing complexity

##### Black box abstraction
- Take something and build a box around it.
- The important thing is that you don't care what is going inside the box.
- Black box abstraction suppresses detail.
- This allows you to go on and build bigger boxes.
	- **Primitive objects**: primitive procedures, primitive data.
	- **Means of combination**: compound procedures, construction of compound data.
	- **Means of abstraction**: procedure definition, simple data abstraction
	- **Capturing common patterns**: higher-order procedures, data as procedures.
	
##### Conventional Interfaces
- Agreed upon ways of connecting things together.
	- generic operations
	- large-scale structure and modularity
	- object-oriented programming
	- operations on aggregates

##### Metalinguistic abstraction
- Another way of controlling complexity is to choose a new design language ( a domain-specific language, or DSL) that will highlight different aspects of the system.
	- It will emphasize some kinds of details and suppress others.
	- This is the technology for building new computer languages.
- The process of interpreting Lisp in Lisp is like a giant wheel of 2 processes:
	- apply 
	- eval
- By using these 2 processes, we can reduce expressions to each other.


## Part 2

#### Three main features
##### Primitive elements:
- Here are some primitive elements in Lisp : `3, 3.14, 5, +`. 
	- These are all names that represent things.
	- The first 3 represent numbers and the last one represents the concept of addition.

##### Means of combination:
- We can take the sum using a combination: `(+ 3 3.14 5)`
- Combination means applying operator to operands
- The operator and the operands themselves can be combinations. 
	- So combinations can be nested
	- Nested combinations can be modeled as *trees*.
- Lisp uses fully parenthesized (unambiguous) prefix notation.
	- Parentheses are just a way to **write trees as a linear sequence of characters**.

##### Means of abstraction:
- This is accomplished in Lisp with `define`
- Defining something gives a name to an expression.
- We write `define` as the same way we write a combination, but `define` is not a combination - it is a *special form*.

- We can use `define` to define a name for a procedure as follows:
```Scheme
(define (square x) (* x x))
```

- We can also make it more clear that we are naming something:
```Scheme
(define square (lambda (x) (* x x)))
```

- The former notation is just a syntactic sugar for the latter.
	- a more convenient surface form for typing 
	- The former de-sugars to the latter.
	
- In Lisp, you don't make arbitrary distinctions between things that are defined in the language and things that happen to be built-in.

#### Case Analysis
- We do case analysis in Lisp using <mark style="background: #FFB86CA6;">cond</mark>
```Scheme
(define (abs x)
  (cond ((< x 0) (- x)
		((= x 0) 0)
		((> x 0) x)))
```
- Each line is a clause consisting of a predicate (true or false) and an action.
- You can do it with `if` keyword, if you have only 2 alternatives:
```Scheme
(define (abs x)
  (if (< x 0)
	  (- x)
	  x))
```

#### Recursion
- We know enough to implement any numerical procedure that you could implement in other languages.
- We don't need any looping constructs in Lisp. We can define things in terms of themselves using recursion.

#### Block Structure
- We can create a black box by packaging internals inside of a definition. This is called *block structure*
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
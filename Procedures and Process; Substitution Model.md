---
share: true
---
up:: [SICP](./SICP.md)
tags:: #procedures #processes #substitution_model #peano #hanoi

# Procedures and Process; Substitution Model
## Part 1
#### Programs and processes
- The job of a programmer is to design processes that accomplish particular goals, like finding the square root of a number.
- You do this by constructing spells (procedures, expressions) which direct a process to accomplish the desired goal.
- You must understand the relation between the particular spells you cast and the process you are trying to control.
- How do particular patterns of procedures and expressions cause particular patterns of execution and behavior in the process?

#### Kinds of expressions
- So far we've seen three main kinds of expressions:
	 - numbers
	 - symbols
	 - combinations
- These are also expressions, but they are *special forms*, so we will worry about them later:
	- lambdas
	- definitions
	- conditionals

#### Evaluating combinations
- These are the substitution rules for evaluating a combination:
	- Evaluate the operator to get the procedure
	- Evaluate the operands to get the arguments
	- Apply the procedure to the arguments
		- Copy the body of the procedure
		- Substitute the arguments supplied for the formal parameters of the procedure.
		- Evaluate the resulting body.

#### Example for evaluation of combinations
- The `sos` procedure takes the sum of the squares:
```Scheme
(define (sq a) (* a a))
(define (sos x y) (+ (sq x) (sq y)))
```

- Let's evaluate the sum of the square of 3 and the square of 4:

```Scheme
(sos 3 4)
(+ (sq 3) (sq 4))
(+ (sq 3) (* 4 4))
(+ (sq 3) 16)
(+ (* 3 3) 16)
(+ 9 16)
25
```
- This is not a perfect description of what the computer/interpreter does. But it is a good model for now.


> [!INFO] Important
> - One of the things we have to learn how to do is ignoring details. The key to understanding complicated things is to know what not to look at, and what not to compute, and what not to think.!!!

#### Evaluating conditionals

- To evaluate 
```Scheme
(if (<predicate>)
	(<consequent>)
	(<alternative>))
```
 - Evaluate the predicate expression
	 - If it yields true, evaluate the consequent expression
	 - If it yields false, evaluate the alternative expression.


#### Example of evaluation of conditionals

- The plus operator in Peano arithmetic uses a conditional:

```Scheme
(define (-1+ x) (- x 1))
(define (1+ x) (+ x 1))

(define (plus x y)
  (if (= x 0)
      y
      (plus (-1+ x) (1+ y))))
```

- Now we can evaluate (+ 3 4) like so:
```Scheme
(plus 3 4)
(if (= 3 0) 4 (plus (- 3 1) (+ 4 1)))
(plus (- 3 1) (+ 4 1))
(plus 2 5)
(if (= 2 0) 5 (plus (- 2 1) (+ 5 1)))
(plus (- 2 1) (+ 5 1))
(plus 1 6)
(if (= 1 0) 6 (plus (- 1 1) (+ 6 1)))
(plus (- 1 1) (+ 6 1))
(plus 0 7)
(if (= 0 0) 7 (plus (- 0 1) (+ 7 1)))
7
```


## Part 2
#### Pre-visualization
- Programs are made of procedures and expressions, and they evolve processes.
- But how do particular programs evolve particular processes?
- We want to go from particularly shaped programs to particularly shaped processes.
- We want to pre-visualize the process like a photographer pre-visualizes the photo before taking the shot.

#### Peano arithmetic
- There are 2 ways to add whole numbers in Peano arithmetic.
- 1st way:
```Scheme
(define (plus x y)
  (if (= x 0)
      y
      (plus (-1+ x) (1+ y))))
```
- This one generates an linear iterative process with O(n) time and O(1) space.
```Scheme
>(plus 3 4)
>(plus 2 5)
>(plus 1 6)
>(plus 0 7)
<7
```
- 2nd way:
```Scheme
(define (plus x y)
  (if (= x 0)
      y
      (1+ (plus (-1+ x) y))))
```
- This one generates a linear recursive process with O(n) time and O(n) space
```Scheme
>(plus 3 4)
> (plus 2 4)
> >(plus 1 4)
> > (plus 0 4)
< < 4
< <5
< 6
<7
```

 - The iteration has all of its state in explicit variables. The recursion doesn't.

## Part 3

#### Perturbation analysis
- Make small changes to the program and see how it affects the process.

#### Fibonacci sequence
- We can represent the Fibonacci numbers 0,1,1,2,3,5,8,13,21,...
```Scheme
(define (fib n)
  (if (< n 2)
      n
      (+ (fib (- n 1))
         (fib (- n 2)))))
```
- This is a tree-recursive process. 
	- We can represent the evaluation with a tree.
	- This is also a terribly inefficient process because there is so much redundant computation.


> [!INFO] Highlights
> And the reason why people think of programming as being hard, of course, is because you are writing down a general rule, which is going to be used for lots of instances.
> You have got to write down something that's general in terms of variables, and you have to think of all the things that could possibly fit in those variables, and all those have to lead to the process you want to work.

#### Towers of Hanoi


> [!INFO] Highlights
>The way in which you would construct a recursive process is by wishful thinking. You have to believe.

- Move an n-high tower from spike `from` to spike `to` using spike `spare`.
```Scheme
#lang racket
(define (hanoi n from to spare)
  (cond ((= n  0) (display "\n"))
        (else (hanoi (- n 1) from spare to)
              (printf "Moving disk ~a from rod ~a to rod ~a\n" n from to)
              (hanoi (- n 1) spare to from))))
```

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
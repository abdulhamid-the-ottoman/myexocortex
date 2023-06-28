---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #linear_recursion_and_iteration #sicp/ch1 

# Linear Recursion and Iteration
- The factorial of N is defined as the product of integers on the interval. \[1,N\]

- The naive recursive implementation creates a curved shape:
```Scheme
(define (factorial n)
  (if (= n 1)
      1
      (* n (factorial (- n 1)))))
```

```Scheme
(factorial 4) 
(* 4 (factorial 3)) 
(* 4 (* 3 (factorial 2))) 
(* 4 (* 3 (* 2 (factorial 1))))
(* 4 (* 3 (* 2 1))) 
(* 4 (* 3 2))
(* 4 6) 
24
```

- The iterative implementation maintains a running product and multiplies the numbers from 1 to N. This creates a shape with a straight edge:

```Scheme
(define (factorial n)
  (fact-iter 1 1 n))

(define (fact-iter count product num)
  (if (> count num)
      product
      (fact-iter (+ count 1) (* product count) num)))
```

```Scheme
(factorial 4) 
(fact-iter 1 1 4) 
(fact-iter 1 2 4) 
(fact-iter 2 3 4)
(fact-iter 6 4 4) 
(fact-iter 24 5 4)
24
```

- Both compute the same mathematical function, but the computational processes evolve very differently.
- The first one is a *linear recursive process*. The chain of deferred operations causes an expansion (as operations are added) and a contraction (as operations are performed).
	- The interpreter must keep track of all these operations.
	- It is a linear recursive process because the information it must keep track of (the call stack) grows linearly with N.
- The second one is a *linear iterative process*. It doesn't grow and shrink.
	- It is summarized by a fixed number of state variables and a rule to describe how they should update and when the process should terminate.
	- It is a linear iterative process because the number of steps grows linearly with N.
- In the iterative process, the variables provide a complete description of the state of the process at any point.
	- in fact-iter above, we only needed 3 variables to keep the state.
- In the recursive process, there is "hidden" information that makes it impossible to resume the process midway through.
	- The longer the chain of deferred operations, the more information must be maintained(in a stack).
- A recursive procedure is simply a procedure that refers to itself directly or indirectly.
- A recursive process refers to the evolution of the process described above.
- A recursive procedure can generate an iterative process in Scheme thanks to tail-call optimization.
	- In other languages (C, C++, Java), special purpose looping constructs (for, while and etc) are needed. 
	- fact-iter generated an iterative process even though it is recursive procedure.

---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [Exercise 9](./SICPE%201.09.md)
- [Exercise 10](./SICPE%201.10.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
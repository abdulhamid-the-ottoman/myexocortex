---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #squareroot_method #sicp/ch1 

# Square Roots by Newton's Method

> [!INFO] The Difference
>  There is an important difference between mathematical functions and computer procedures. Procedures must be effective 

- In mathematics, you can define square roots by saying, "The square root of x is the nonnegative y such that $y^2$ = x ". This is not a procedure.
- Mathematical functions describe what things are. (*declarative knowledge*) ; procedures describe how to do things (*imperative knowledge*)
- **Declarative is "what is" and imperative is "how to"**

- Newton's method for square roots says
	- Whenever we have a guess y for the value of the square root of a number x, we can perform a simple manipulation to get a better guess (one closer to the actual square root) by averaging y with x/y.

```Scheme
#lang sicp

(define (sqrt x)
  (sqrt-iter 1.0 x))

(define (sqrt-iter guess x)
  (if (good-enough? guess x)
      guess
      (sqrt-iter (improve guess x) x))) ; recursive

(define (improve guess x)
  (average guess (/ x guess)))

(define (average x y)
  (/ (+ x y) 2))

(define (good-enough? guess x)
  (< (abs (- (square guess) x)) 0.001))

(define (square x)
  (* x x))

(define (abs x)
  (if (< x 0)
      (- x)
      x))

(sqrt 2) ; 1.4142156862745097
```

^23697c


---

## 🔑 Key Points
- An important current area in PL design is the exploration of so-called very high level languages, in which one actually programs in terms of declarative statements.
	- The key idea is to make interpreters sophisticated enough so that, given "what is" knowledge specified by the programmer, the interpreters can generate "how to" knowledge automatically.
## ❓ Questions
- 
## 📦 Resources
- [Exercise 6](./SICPE%201.06.md)
- [Exercise 7](./SICPE%201.07.md)
- [Exercise 8](./SICPE%201.08.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
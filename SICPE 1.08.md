---
created: ["2023-06-12 12:09"]
share: true
---

up::[SICP-Chapter1-Exercises](./SICP-Chapter1-Exercises.md)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Newton’s method for cube roots is based on the fact that if y is an approximation to the cube root of x, then a better approximation is given by the value
> ![Pasted image 20230612121014.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230612121014.png)
> Use this formula to implement a cube-root procedure analogous to the square-root procedure.

## 🔑 **Key Points of Understanding**

# 🔍 Solutions
```Scheme
#lang sicp

(define (cube-root x)
  (cube-root-iter 1.0 x))

(define (good-enough? previous current)
  (< (/ (abs (- previous current)) current) 0.0000000001))

(define (square x)
  (* x x))


(define (improve y x)
    (/ (+ (/ x (square y)) (* 2 y)) 3))


(define (cube-root-iter guess x)
  (if (good-enough? guess (improve guess x))
      guess
      (cube-root-iter (improve guess x) x)))

(cube-root 27) ; 3.0000000000000977
```

# 🧠 Ideas about Problem

# 🔗 Related Applications


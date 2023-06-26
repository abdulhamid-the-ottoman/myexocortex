---
created: ["2023-06-12 07:29"]
share: true
---

up::

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Define a procedure that takes three numbers as arguments and returns the sum of the squares of the two larger numbers.

## 🔑 **Key Points of Understanding**

# 🔍 Solutions
```Scheme
#lang sicp

(define (min2 a b)
  (if (< a b)
      a
      b))

(define (min3 a b c)
  (min2 (min2 a b) c)
  )

(define (square x)
  (* x x))

(define (sum-of-squares a b)
  (+ (square a) (square b)))


(define (f a b c)
  (cond ((= a (min3 a b c)) (sum-of-squares b c))
        ((= b (min3 a b c)) (sum-of-squares a c))
        (else (sum-of-squares a b))))

(f 3 4 5)
```
# 🧠 Ideas about Problem
- Pay attention how you defined min3 in terms of min2
- Pay attention how you excluded min using cond in procedure f.
# 🔗 Related Applications


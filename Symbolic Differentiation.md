---
share: true
---

up:: [ Symbolic Data](./SICP.md#^369430)
tags:: #symbolic_differentiation



# Symbolic Differentiation

- Let's design a procedure that computes the derivative of an algebraic expression.
- This will demonstrate both symbol manipulation and data abstraction.

> [!INFO]  Language For Symbol Manipulation
>  - Symbolic differentiation is of special historical significance in Lisp.
>  - It was one of motivating examples behind the development of a computer language for symbol manipulation.

## The differentiation program with abstract data

- To start, we will only consider addition and multiplication.
- We need three differentiation rules: 
	- constant
	- sum
	- product
- Let's assume we already have these procedures:

| Procedure                | Result                                 |
| ------------------------ | -------------------------------------- |
| `(variable? e)`          | Is `e` a variable?                     |
| `(same-variable? v1 v2)` | Are `v1` and `v2` the same variable?   |
| `(sum? e)`               | Is `e` a sum?                          |
| `(addend e)`             | Addend of the sum `e`                  |
| `(augend e)`             | Augend of the sum `e`                  |
| `(make-sum a1 a2)`       | Construct the sum of `a1` and `a2`     |
| `(product? e)`           | Is `e` a product?                      |
| `(multiplier e)`         | Multiplier of the product `e`          |
| `(multiplicand e)`       | Multiplicand of the product `e`        |
| `(make-product m1 m2)`   | Construct the product of `m1` and `m2` |
|                          |                                        |

- Then, we can express the differentiation rules like so
```Scheme
#lang sicp

(define (deriv exp var)
  (cond ((number? exp) 0)
        ((variable? exp) (if (same-variable? exp var)
                             1
                             0))
        ((sum? exp) (make-sum (deriv (addend exp)
                                     var)
                              (deriv (augend exp)
                                     var)))

        ((product? exp)
         (make-sum (make-product (multiplier exp)
                                 (deriv (multiplicand exp) var))
                   (make-product (deriv (multiplier exp) var)
                                  (multiplicand exp))))
        (else (error "unknown expression type" exp))))
```

## Representing algebraic expressions
- There are many ways we could represent algebraic expressions
- The most straightforward way is parenthesized Polish notation: Lisp syntax
- We can simplify answers in the constructor just like in the `rational number` example
- Simplifying the same way a human would is hard, partly because the most "simplified" form is sometimes subjective.
---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [ Exercise 56](SICPE%202.56.md)
- [ Exercise 57](SICPE%202.57.md)
- [ Exercise 58](SICPE%202.58.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
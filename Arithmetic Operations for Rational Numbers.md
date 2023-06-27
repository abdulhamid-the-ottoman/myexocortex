---
share: true
---

up:: [ Introduction to Data Abstraction](./SICP.md#^0a8a89)
tags:: #rational_numbers 



# Arithmetic Operations for Rational Numbers
- We want to add, subtract, multiply, divide and test equality with our rational numbers
- Assume we have `(make-rat n d)` , `(numer x)` and `(denom x)` available as the constructor and selectors.
	- This is wishful thinking and it is a good technique.
- Here is the implementation for addition:
```Scheme
(define (add-rat x y)
  (make-rat (+ (* (numer x)
                  (denom y))
               (* (numer y)
                  (denom x)))
            (* (denom x)
               (denom y))))
```

## Pairs
- A pair is a concrete structure that we create with `cons`
- We extract the parts of the pair with `car` and `cdr`
- Here is an example:
```Scheme
(define x (cons 1 2)) 
(car x) ;; → 1
(cdr x) ;; → 2
```

- This is all the glue we need to implement all sorts of complex data structures
- Data objects constructed from pairs are called **list-structured data**

## Representing rational numbers
- Now we can represent rational numbers:
```Scheme
(define (make-rat n d) (cons n d))
(define (numer x) (car x)) 
(define (denom x) (cdr x))
```

- To ensure that our rational numbers are always in lowest terms, we need `make-rat` to divide the numerator and denominator by their greatest common divisor (GCD)

```Scheme
(define (make-rat n d) 
  (let ((g (gcd n d))) 
  (cons (/ n g) (/ d g))))
```
---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
-  [ Exercise 1](SICPE%202.1.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
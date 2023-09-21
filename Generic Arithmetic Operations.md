---
share: true
---

up:: [ Systems with Generic Operations](./SICP.md#^daebf9)
tags:: #generic_arithmetic_operations



# Generic Arithmetic Operations
- We want `add` to work for primitive, rational, and complex numbers
- We will attach a type tag to each kind of number. 
	- Complex numbers will have 2 levels of tagging: a `'complex` tag on top of the `'rectangular` or `'polar` tag.
- Tags get stripped off as the data is passed down through packages to the appropriate specific procedure.

```Scheme
(define (add x y) (apply-generic 'add x y))
(define (sub x y) (apply-generic 'sub x y))
(define (mul x y) (apply-generic 'mul x y))
(define (div x y) (apply-generic 'div x y))
```

- Here is the arithmetic package for Scheme numbers:

```Scheme
(define (install-scheme-number-package)
  (define (tag x)
    (attach-tag 'scheme-number x))
  (put 'add '(scheme-number scheme-number)
       (lambda (x y) (tag (+ x y))))
  (put 'sub '(scheme-number scheme-number)
       (lambda (x y) (tag (- x y))))
  (put 'mul '(scheme-number scheme-number)
       (lambda (x y) (tag (* x y))))
  (put 'div '(scheme-number scheme-number)
       (lambda (x y) (tag (/ x y))))
  (put 'make 'scheme-number
       (lambda (x) (tag x)))
  'done)

(define (make-scheme-number n)
  ((get 'make 'scheme-number) n))
```

- We can implement similar packages for rational and complex numbers

---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [ Exercise 77](SICPE%202.77.md)
- [ Exercise 78](SICPE%202.78.md)
- [ Exercise 79](SICPE%202.79.md)
- [ Exercise 80](SICPE%202.80.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #compound_procedures #sicp/ch1 

# Compound Procedures
- *Procedure definition* is a powerful technique for abstraction
- General from of a procedure definition is:
```Scheme
(define (_name_ _formal-parameters_) _body_)

```
 - if the body contains more than one expression, each is evaluated in sequence and the value of the last one is returned.

- Here is a *compound procedure* given the name square along with another one called sum-of-squares.
```Scheme
(define (square x) (* x x))
(define (sum-of-squares x y) (+ (square x) (square y)))
```

- Compound procedures shown above are used in exactly the same way as primitive procedures such as + or \*.

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

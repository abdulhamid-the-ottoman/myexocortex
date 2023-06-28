---
share: true
---

up:: [ Multiple Representations for Abstract Data](./SICP.md#^b0aa29)
tags:: #tagging_data

# Tagged Data
- One way to view data abstraction is as the *principle of least commitment*.
	- Wait until last minute to choose a concrete representation, retaining maximum flexibility.
	- We can take it even further and avoid committing to a single representation at all.
		- To do this, we need some way of distinguishing between representations.
		- We will do this using a *type tag* `'rectangular` and `'polar`
- Each generic selector will strip off the type-tag and use case analysis to pass untyped data object to the appropriate specific selector.

```Scheme
(define (attach-tag type-tag contents)
  (cons type-tag contents))
(define (type-tag datum)
  (if (pair? datum)
      (car datum)
      (error "bad tagged datum" datum)))
(define (contents datum)
  (if (pair? datum)
      (cdr datum)
      (error "bad tagged datum" datum)))

(define (rectangular? z)
  (eq? (type-tag z) 'rectangular))
(define (polar? z)
  (eq? (type-tag z) 'polar))
```

^4bd777

- For example, here is how we implement the generic `real-part`
```Scheme
(define (real-part z)
  (cond ((rectangular? z) (real-part-rectangular (contents z)))
        ((polar? z)  (real-part-polar (contents z)) )
        (else (error "unknown representation" z))))
```

^2c42d5

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
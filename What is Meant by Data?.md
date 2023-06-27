---
share: true
---

up:: [SICP](./SICP.md)
tags:: #what_is_data

# What is Meant by Data?

- Data is defined by some collection of *selectors* and *constructors*, together with specified conditions that these procedures must fulfill in order to be a valid representation.

- For rationals, we have the following definition:
	- We can construct a rational `x` with `(make-rat n d)`
	- We can select the numerator with `(numer x)`
	- We can select the denominator with `(denom x)`
	- For all values of  `x` , `(/ (numer x) (denom x))` must be equal n/d

- For pairs, it is even simpler: we need 3 operations, which we will call `cons`, `car`, and `cdr` , such that if z is `(cons x y)` , then `(car z)` is `x` and `(cdr z)` is `y`.
- Any triple of procedures satisfying this definition can be used to implement pairs.

	- In fact we can do it with procedures themselves:
	```Scheme
	(define (cons x y) ;; pay attention we are returning a procedure
	  (lambda (m)
	    (if (= m 0)
	        x
	        y)))

	(define (car z) (z 0)) ;; we are using it
	(define (cdr z) (z 1))
	```

	- This doesn't look like data, but it works
	- This is how you implement pairs in $\lambda$ calculus
	- In real Lisp implementations, pairs are implemented directly, for reasons of efficiency.
		- They could be implemented as shown above, nobody would be able to tell the difference

> [!INFO]  Representing Compound Data
>  - The ability to manipulate procedures as objects automatically provides the ability to represent compound data
---

- This style of programming is often called **message passing**
---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [ Exercise 4](SICPE%202.4.md)
- [ Exercise 5](SICPE%202.5.md)
- [ Exercise 6](SICPE%202.6.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
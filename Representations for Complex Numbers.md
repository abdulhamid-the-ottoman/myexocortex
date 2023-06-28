---
share: true
---

up:: [ Multiple Representations for Abstract Data](./SICP.md#^b0aa29)
tags:: #complex_number_representations



# Representations for Complex Numbers
- A complex number  can be mathematically represented in 2 ways :
	 ![200](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230627151756.png)
- So we can represent a complex number in 2 ways:
	- rectangular form (x,y)
	- polar form (r,$\theta$)
- Rectangular form is convenient for addition and subtraction
- Polar form is convenient for multiplication and division
- Our goal is to implement all the operations to work with either representation:

```Scheme
(define (add-complex z1 z2)
  (make-from-real-imag (+ (real-part z1) (real-part z2))
                       (+ (imag-part z1) (imag-part z2))))
(define (sub-complex z1 z2)
  (make-from-real-imag (- (real-part z1) (real-part z2))
                       (- (imag-part z1) (imag-part z2))))
(define (mul-complex z1 z2)
  (make-from-mag-ang (* (magnitude z1) (magnitude z2))
                     (+ (angle z1) (angle z2))))
(define (div-complex z1 z2)
  (make-from-mag-ang (/ (magnitude z1) (magnitude z2))
                     (- (angle z1) (angle z2))))
```

- We can implement the constructors and selectors to use rectangular form or polar form, 
	- but how do we allow both?

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
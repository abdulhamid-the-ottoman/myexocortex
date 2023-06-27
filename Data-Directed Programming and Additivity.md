---
share: true
---
up:: [ Multiple Representations for Abstract Data](./SICP.md#^b0aa29)
tags:: #data-directed-programming #additivity

# Data-Directed Programming and Additivity
- The strategy of calling a procedure based on the type tag is called *dispatching on type*
- The implementation in [Generic Real-Part](./Tagged%20Data.md#^2c42d5) has  2 significant weakness:
	- The generic procedures must know about all the representations.
		- polar, rectangular, some other new representations
	- We must guarantee that no 2 procedures have the same name
		- real-part-polar, real-part-rectangular
- The underlying issue is that the technique is not *additive*
- The solution is to use a technique known as *data-directed programming*
- Imagine a table with operations on one axis and types on the other axis:

|                | Polar             | Rectangular             |
| -------------- | ----------------- | ----------------------- |
| Real part      | `real-part-polar` | `real-part-rectangular` |
| Imaginary part | `imag-part-polar` | `imag-part-rectangular` |
| Magnitude      | `magntiude-polar` | `magntiude-rectangular` |
| Angle          | `angle-polar`     | `angle-rectangular`     |

- Before, we implemented each generic procedure using case analysis.
	- Now, we will write a single procedure that looks up the operation name and argument type in a table.
- Assume we have the procedure `(put op type item)` which installs `item` in the table and `(get op type)` which retrieves it.

- Then, we can define a collection of procedures, or package, to install the each representation of complex numbers. For example:

```Scheme
(define (install-rectangular-package)
  ;; Internal procedures
  (define (real-part z) (car z))
  (define (imag-part z) (cdr z))
  (define (make-from-real-imag x y) (cons x y))
  (define (magnitude z)
    (sqrt (+ (square (real-part z))
             (square (imag-part z)))))
  (define (angle z)
    (atan (imag-part z) (real-part z)))
  (define (make-from-mag-ang r a)
    (cons (* r (cos a)) (* r (sin a))))

  ;; Interface to the rest of the system
  (define (tag x) (attach-tag 'rectangular x))
  (put 'real-part '(rectangular) real-part)
  (put 'imag-part '(rectangular) imag-part)
  (put 'magnitude '(rectangular) magnitude)
  (put 'angle '(rectangular) angle)
  (put 'make-from-real-imag 'rectangular
       (lambda (x y) (tag (make-from-real-imag x y))))
  (put 'make-from-mag-ang 'rectangular
       (lambda (r a) (tag (make-from-mag-ang r a))))
  'done ;; returns a symbol to indicate it is done)
```

- We use the list (rectangular) rather than the symbol rectangular to allow for the possibility of operations with multiple arguments, not all of the same type. 
	- type-tags come from data types on which the procedures are applied

- The  type of constructors are installed under needn't be a list because a constructor is always used to make an object of one particular type

- One can  implement the same install procedure for the polar part. (e.g install-polar-package)
	- And they can both use their original procedures defined with the same names as each other's (e.g real-part)
	- These definitions are now internal to different procedures, so there is no name conflict.

- Next we need a way to look up a procedure in the table by operation and arguments:

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
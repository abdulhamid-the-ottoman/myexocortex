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
	- We will do this by means of a general "operation" procedure called *apply-generic*, which applies a generic operation to some arguments.

	 ```Scheme
	(define (apply-generic op . args)
	  (let ((type-tags (map type-tag args)))
	    (let ((proc (get op type-tags)))
	      (if proc
	          (apply proc (map contents args))
	          (error "no method for these types" (list op type-tags))))))
	```

	- Pay attention the dot in the argument list-  this is known as *dotted-tail* notation.
		- this is because different generic operations may take different numbers of arguments.
		- In apply-generic, op has as its value the first argument to `apply-generic` and `args` has as its value a list of the remaining arguments
	- `apply-generic` also uses the primitive procedure `apply` , which takes 2 arguments, a procedure and a list.
		- `apply` applies the procedure, using the elements in the list as arguments.
		- `(apply + (list 1 2 3 4))`  returns 10
		
- Using `apply-generic`, we can define our generic selectors as follows:
```Scheme
(define (real-part z) (apply-generic 'real-part z))
(define (imag-part z) (apply-generic 'imag-part z))
(define (magnitude z) (apply-generic 'magnitude z))
(define (angle z) (apply-generic 'angle z))
```

- Observe that the apply-generic choses the right version based on the type-tag of `z`.
- Observe that these do not change at all if a new representation is added to the system.
- We can also extract from the table the constructors to be used by the programs external to the packages in making complex numbers from real and imaginary parts and from magnitudes and angles.

```Scheme
(define (make-from-real-imag x y)
  ((get 'make-from-real-imag 'rectangular) x y))

(define (make-from-mag-ang r a)
  ((get 'make-from-mag-ang 'polar) r a))
```


## Message Passing

^0f73cc

- Data-directed programming deals explicitly with the *operation-and-type table*
- In [Tagged Data](./Tagged%20Data.md#^4bd777), we made "smart operations" that dispatch on type. 
	- This effectively decomposes the table into rows, 
	- with each generic operation procedure representing a row of the table.
- Another approach is to make "smart data objects" that dispatch based on operation names.
	- This effectively decomposes the table into columns.
```Scheme
(define (make-from-real-imag x y)
  (define (dispatch op)
    (cond ((eq? op 'real-part) x)
          ((eq? op 'imag-part) y)
          ((eq? op 'magnitude)
           (sqrt (+ (square x) (square y))))
          ((eq? op 'angle) (atan y x))
          (else (error "unknown op" op))))
  dispatch)
```

- Pay attention what return from the value returned by `make-from-real-img` is a procedure- the internal dispatch procedure.
-  This is called *message-passing*, and we can establish it in Scheme using closures.
	- Why is it called "message-passing" ? 
		- Because a data object is an entity that receives the requested operation name as a "message".
	- Message passing can be a powerful tool for structuring simulation programs
- `apply-generic` procedure applied a generic operation to an argument, now we feed the operation's name to the data object and let the object do the work.
	- One limitation of this organization is it permits only generic procedures of one argument.
	- we can even define single argument apply-generic in terms of message-passing
		`(define (apply-generic op arg) (arg op))`
---

## 🔑 Key Points
- 
## ❓ Questions
-  "Expression problem", how does it relate to apply-generic?
## 📦 Resources
- [ Exercise 73](SICPE%202.73.md)
- [ Exercise 74](SICPE%202.74.md)
- [Message Passing](Data-Directed%20Programming%20and%20Additivity.md#^0f73cc)
	- [ Exercise 75](SICPE%202.75.md)
	- [ Exercise 76](SICPE%202.76.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
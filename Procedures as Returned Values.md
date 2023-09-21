---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #procedures_as_returned_values, #newtons_method #first_class_procedures

# Procedures as Returned Values
- Passing procedures as arguments gives us expressive power.
- Returning procedures from procedures gives us even more expressive power.
- For example, we can write a procedure that creates a new procedure with average damping:

```Scheme
(define (average-damp f)
  (lambda (x) (average x (f x))))
```

- If we use `average-damp` on `square`, we get a procedure that calculates the sum of the numbers from 1 to n:
```Scheme
((average-damp square) 10) ;; 55

(+ 1 2 3 4 5 6 7 8 9 10) ;; 55
```

> [!INFO] The Experienced Programmer
>  - In general, there are many ways to formulate a process as a procedure.
>  - Experienced programmers know how to choose procedural formulations that are particularly perspicuous, and where useful elements of the process are exposed as separate entities that can be reused in other applications.

- Using `average-damp`, we can re-formulate the square-root procedure as follows using `fixed-pt` procedure ![Procedures as General Methods > ^6d0ad9](./Procedures%20as%20General%20Methods.md#^6d0ad9) 
- This is a nice solution to the oscillation problem mentioned here [Procedures as General Methods > ^693fc1](./Procedures%20as%20General%20Methods.md#^693fc1)
	```Scheme
	(define (sqrt x)
		(fixed-pt (average-damp (lambda (y) (/ x y))) 1.0))
	```
	
## Newton's method
- The square root procedure we wrote [Square Roots by Newton's Method](./Square%20Roots%20by%20Newton's%20Method.md) was a special case of newton's method.
- Given a function f(x), the solution to f(x) = 0 is given by the fixed point of
		![300](./40-referenceVAULTS/Resource%20Library/Images/IMG_465DC3C6E83A-1.jpeg)
	-  $\mapsto$ is pronounced as "maps to", is the mathematician's way of writing lambda y $\mapsto$ x/y means `(lambda (y) (/ x y))`, that is, the function whose value at y is x/y
	- This is known as newton transform and can be also given mathematically as
		![300](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230727144614.png)
	- This function finds the $x_2$ shown below using $x_1$
		![Pasted image 20230727142727.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230727142727.png)
	- Finding fixed point iterates this function until you hit the f(x) =x

	 
- Newton's method converges very quickly- much faster than the half-interval method in favorable cases. 
	- We need a procedure to transform a function into its derivative ( a new procedure). We can use a small dx for this:
			![300](./40-referenceVAULTS/Resource%20Library/Images/IMG_EC087598CCAF-1.jpeg)

	 - This translates to the following procedure:
```Scheme
	(define (deriv f)
		(lambda (x) (/ (- (f (+ x dx)) (f x)) dx)))
```

- Like average-damp, deriv is a procedure that takes a procedure as argument and returns a procedure as a value.
	 - Now we can approximate the derivative of x $\mapsto$ $x^3$  at 5 (which is exactly 75), we can evaluate
```Scheme
		(define (cube x) (* x x x))
		((deriv cube) 5) ;; 75.000149
```

- Now , with the aid of `deriv` , we can express Newton's method as a fixed-point process:
	- First we implement the newton function shown in ![100](./40-referenceVAULTS/Resource%20Library/Images/IMG_465DC3C6E83A-1.jpeg) as follows:
		```Scheme
	(define (newton-transform g)
		(lambda (x) (- x (/ (g x) ((deriv g) x)))))
	```
		- This procedure takes a procedure as an argument and computes the function for which we want to find a zero

	- Then we use the `fixed-pt` method to converge with an initial guess:
		```Scheme
	(define newtons-method g guess)
		(fixed-pt (newton-transform g) guess))
	```
       - This function takes the initial guess to find the value which makes it zero.

	- Now we can implement yet another square-root procedure:
```Scheme
	(define (sqrt x)
		(newtons-method (lambda (y) (- (square y) x)) 1.0))
```

## Abstractions and first-class procedures
- Compound procedures let us express general methods of computing as explicit elements in our programming language.
- Higher-order procedures let us manipulate methods to create further abstractions.
- We should always be on the lookout for underlying abstractions that can be brought out and generalized.
	- But this doesn't mean we should always program in the most abstract form possible; there is a level of abstraction which appropriate to each task.
- Elements with the fewest restrictions are first-class:
	- They may be named by variables.
	- They may be passed as arguments to procedures
	- They may be returned as the results of procedures
	- They may be included in data structures.
- In Lisp, procedures have first-class status. This gives us an enormous gain in expressive power
---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [Exercise 40](SICPE%201.40.md)
- [Exercise 41](SICPE%201.41.md)
- [Exercise 42](SICPE%201.42.md)
- [Exercise 43](SICPE%201.43.md)
- [Exercise 44](SICPE%201.44.md)
- [Exercise 45](SICPE%201.45.md)
- [Exercise 46](SICPE%201.46.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
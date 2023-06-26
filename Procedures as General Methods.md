---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #procedures_as_general_methods #half_interval_method #fixed_point_of_functions

# Procedures as General Methods
- So far, we have seen:
	- Compound procedures that abstract patterns of numerical operators (mathematical functions), independent of the particular numbers. 
		- instead of calculating square of 5 alone, we write a compound procedure to calculate the square of any number..
	- Higher-order procedures that express a more powerful kind of abstraction, independent of the procedures involved.
		- instead of writing a summation procedure for every case needed, we abstracted the concept of summation and took the required term and next functions as formal parameters.
		
- Now we will take it a bit further:

## Finding roots of equations by half-interval method

- The *half-interval method* : a simple but powerful technique for solving `f(x) = 0`
- Given `f(a) < 0 < f(b)`, there must be at least one zero between a and b.
- To narrow it down, we let x be the average of a and b, and then replace either left bound or the right bound with it.
```Scheme
#lang sicp

(define (average a b) (/ (+ a b) 2.0))

(define (close-enough? a b) (< (abs (- a b)) 0.001))

(define (search f n p)
  (let ((midpt (average n p)))
    (if (close-enough? n p)
        midpt
        (let ((test-val (f midpt)))
          (cond ((positive? test-val)
                 (search f n midpt))
                
                ((negative? test-val)
                 (search f midpt p))

                (else midpt))))))

(define (half-interval-method f a b)
  (let ((a-val (f a))
        (b-val (f b)))
    (cond ((and (negative? a-val)
                (positive? b-val))
           (search f a b))
          
          ((and (negative? b-val)
                (positive? a-val))
           (search f b a))
          
          (else (error "f(a) and f(b) must be of opposite signs" a b)))))

; We can use half-interval-method to approximate pi as root of sin x = 0 
(half-interval-method sin 2.0 4.0)
```

## Finding Fixed points of functions
- A number x is a fixed point of a function if f(x) = x
- In some cases, repeatedly applying the function to an arbitrary initial guess will converge on the fixed point.
	- f(f(f(f ...... (x)))) = x
- The procedure we made earlier for finding square roots is actually a special case of the fixed point procedure.
	- ![Square Roots by Newton's Method > ^23697c](./Square%20Roots%20by%20Newton's%20Method.md#^23697c)
- Let'`s implement this function:
```Scheme
#lang sicp

(define tolerance 0.00001)
(define (fixed-pt f initial-guess)
  
  (define (close-enough? a b) ;; ending condition
    (< (abs (- a b))
       tolerance))
       
  (define (iter guess) ; f(f(f(...)))
    (let ((next (f guess)))
      (if (close-enough? next guess)
        next
        (iter next))))
        
  (iter initial-guess)
 )

(fixed-pt cos 1.0); 0.739
```

^6d0ad9

## 🔑 Key Points
- 
## ❓ Questions
- Think and learn how square root is a special case of finding fixed point?
	-  Computing the square root of some number of x requires finding a y such that $y^2$ = x
	- Putting the equation into *equivalent form* y = $\frac{x}{y}$
	- Then we try to compute it as follows:
		```Scheme
		(define (sqrt x)
		  (fixed-pt (lambda (y) (/ x y)) 1.0))
		(sqrt 2.0)
```
	- Unfortunately, this fixed-pt search doesn't converge.! Why?
		- Consider the initial guess $y_1$ Let's assume that next guess is $y_2$ = $\frac{x}{y_1}$
		- Then the next next $y_3$ = $\frac{x}{y_2}$ = $\frac{x}{\frac{x}{y_2}}$ = $y_2$, so it loops around!. This will *oscillate* about the answer.
	- So we need a way to control this oscillations. going back and forth between 2 points causes this problem
		- We know that our answer is between x and x/y , so we want to make a new guess that is not as far from y as x/y by averaging y with x/y.
			- y  = $\frac{1}{2}$(y + x/y)
		- But we have to make sure that we don't violate the original function :
			- y = $\frac{x}{y}$ , to do that we add y to both sides and divide it by 2, we have 2y = y+ (x/y) -> y  = $\frac{1}{2}$(y + x/y)
		- This approach of averaging successive approximations to a solution, a technique that we call *average damping*, often aids the convergence of fixed-point searches.
## 📦 Resources
- [Exercise 1.35](Exercise%201.35.md)
- [Exercise 1.36](Exercise%201.36.md)
- [Exercise 1.37](Exercise%201.37.md)
- [Exercise 1.38](Exercise%201.38.md)
- [Exercise 1.39](Exercise%201.39.md)
## 🎯 Actions
- [x] Answer the questions in the questions section
- [ ] 
- [ ] 
- [ ] 
- [ ] 

^693fc1

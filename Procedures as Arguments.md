---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #procedures_as_arguments

# Procedures as Arguments
- Procedures that compute a sum can take many forms such as:
	- sum of integers from a through b:
		```Scheme
	#lang sicp
	(define (sum-integers a b)
		(if (> a b)
		    0
		    (+ a (sum-integers (+ 1 a) b))))
		
	(sum-integers 1 5) ; 15
	```
	- sum of cubes of the integers in the given range:
		```Scheme
	(define (cube x) (* x x x))
	(define (sum-cubes a b)
		(if (> a b)
			0
		    (+ (cube a) (sum-cubes (+ a 1) b))))

	(sum-cubes 1 3) ;36
```
	 - sum of a sequence of terms in the series which converges to $\frac{\pi}{8}$ :
	 ```Scheme
	(define (pi-sum a b)
		(if (> a b)
	      0
	      (+ (/ 1.0 (* a (+ a 2)))
	         (pi-sum (+ a 4) b))))

	(* 8 (pi-sum 1 300)) ; 3.134926060993086
```
- If you pay close attention, you would see that their form is very similar, and we can represent them with the following form:

	```Scheme
(define (<name> a b)
  (if (> a b)
      0
      (+ (<term> a) ; a term calculation
         (<name> (<next> a) b))))  ; recursive call with the next value
```

	- This is a useful abstraction, just as the sigma notation $\Sigma$ (symbol for summation) in math because the summation of series is so common.
		![300](Pasted%20image%2020230616183654.png)
	- The power of sigma notation is that it allows mathematicians to deal with the concept of summation itself rather than only with particular sums.
	
- Now, as programmers we are nothing short of mathematicians, we would like our language to be powerful enough so that we can *write a procedure that expresses the concept of summation* itself rather than *only procedures that compute particular sums such as* **sum-integers** , **sum-cubes** and **pi-sum**
	- Here is how we  abstract the concept of summation:
	```Scheme
		(define (sum term a next b)
		  (if (> a b)
		      0
		      (+ (term a)
		         (sum term (next a) next b))))
	```

	- Here is how we use it to sum integers a through b:
		```Scheme
		(define (inc n) (+ n 1))
		(define (identity x) x)
		(sum identity 1 inc 10) ; 55
	  ```

	 - Here is how we do it for pi-sum:
	 ```Scheme
		(define (pi-term a) (/ 1.0 (* a (+ a 2))))
		(define (pi-next a) (+ a 4))
		(* 8 (sum pi-term 1 pi-next 300)) ; 3.134926060993086
	```
 
- We can use this sum as a building block in formulating further concepts such as the definite integral of a function f between the limits a and b can be approximated numerically using the following formula:

	![Pasted image 20230616212533.png](Pasted%20image%2020230616212533.png)

	- We can express this procedure directly as a procedure:
	 ```Scheme
		(define (integral f a b dx)
			(define (add-dx x)
			    (+ x dx))
			(* (sum f 
					(+ a (/ dx 2.0)) 
					add-dx 
					b) 
				dx))

		(integral cube 0 1 0.01) ; 0.24998750000000042
	```
---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [Exercise 29](SICPE%201.29.md)
- [Exercise 30](SICPE%201.30.md)
- [Exercise 31](SICPE%201.31.md)
- [Exercise 32](SICPE%201.32.md)
- [Exercise 33](SICPE%201.33.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #lambda #let

# Constructing Procedures Using Lambda
- `lambda` creates anonymous procedures.
	- They are just like the procedures created by `define`, but without a name
	 ```Scheme
	(lambda (formal-parameters) body)
	```

- A lambda expression can be used as the operand in a combination. It will be evaluated to a procedure and applied to the arguments( the evaluated operands).
	- The name comes from the $\lambda$ - calculus, a formal system invented by Alonzo Church.
	
- Here is an example
	 ```Scheme
	(lambda (x y z) (+ x y (square z)))
	```
	- We can even use this lambda procedure as a operator as follows:
	 ```Scheme
	((lambda (x y z) (+ x y (square z))) 1 2 3) ; 12
	```

- You can even name these nameless procedures using define as is there is no difference following two:
	```Scheme
		(define (plus4 x) (+ x 4))
		(define plus4 (lambda (x) (+ x 4)))
	```

## Using let to create local variables
- We often need local variables in addition to the formal parameters. Here is an example:
	 ![Pasted image 20230616214352.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230616214352.png)
	 - We can write the equation above as follows:
				 ![300](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230616214445.png)
	 - This shows us that we need local variables a and b to be used in procedure f.

- We can do this in 2 ways:
	- With an auxiliary procedure to bind local variables:
	
		```Scheme
	  (define (f x y)
			(define (f-helper a b) ; here are our local variables
				    (+ (* x (square a))
				       (* y b)
				       (* a b)))
			(f-helper (+ 1 (* x y)
		            (- 1 y))))
	  ```
	  
	- With a lambda expression that takes the local variables as arguments, 
	  ```Scheme
	  (define (f x y)
		  ((lambda (a b)
		    (+ (* x (square a))
		       (* y b)
		       (* a b))) (+ 1 (* x y))
		                (- 1 y)))
	 ```
	
- However this is so common that there is a special form `let` to make it easier. Here is the general form of a let-expression:
	```Scheme
	(let ((<var1> <exp1>)
		  (<var2> <exp2>)
		  ...
		  (<varn> <expn>))
	<body>)
	```
- And as you may have already guessed this a syntactic sugar for:

```Scheme
	((lambda (<var1> <var2> ... <varn>)
		body)
	<exp1>
	<exp2>
	...
	<expn>)
```

- The scope of a variable in a let-expression is the body. This allows variables to be bound as locally as possible
```Scheme
(let ((x 3)
      (y 2))
  (display (+ x y)) ; 5
  (display "\n")
  (let ((x 5) ; x = 5
        (y (* x y))) ; y = 3 * 2
    (display (+ x y)) ; 11
    (display "\n")
    )
  (display (+ x y)) ; 5
)
```
- The variables in the let-expression are parallel and independent. They can't refer to each other, and their order doesn't matter.
	- From the example above, you can see that in the inner let, while defining new variable y, on the right hand side of the equal sign, x and y are used from the outer scope.
	- This is the expected behavior because, you are actually calling a lambda procedure with real argument of (* x y)
- You can use let-expressions instead of internal definitions:
	```Scheme
	(define (f x y)
		(define a (+ 1 (* x y)))
		(define b (- 1 y))
		(+ (* x (square a))
		   (*  y b)
		   (* a b)))
	```
	- For now, we use let to define variables, and use internal define only for internal procedures -> soon to be cleared why?
---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [Exercise 34](SICPE%201.34.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
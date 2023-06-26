---
share: true
---
up:: [The Elements of Programming](./The%20Elements%20of%20Programming.md)
tags:: #expressions, #sicp/ch1 

# Expressions
- The REPL (Read-Eval-Print-Loop)
	- **(R)eads** an expression
	- **(E)valuates** the expression
	- **(P)rints** the result
	- **(L)oop** back to do the same

- A number is one kind of *primitive expression*.
	- More precisely, the expression that you type consists of the numerals that represents the number in base 10. 
	- Ex: 574 is an expression composed of numerals 5, 7 and 4 which represents the number five hundred and seventy four.

- An application of a *primitive procedure* (such as + or \*)  to  numbers is one kind of *compound expression*.
```Scheme
#lang sicp

(+ 137 349)    ;486
(- 1000 334)   ;666
(* 5 99)       ;485
(/ 10 4)       ;2 1/2
(/ 10 4.0)     ;2.5
(+ 2.7 10)     ;12.7
```

- A *combination* denotes procedure application by a list of expressions inside parentheses. example: (/ 10 4)
	- The first element is the *operator*
	- The rest are the *operands*.
	- The *value of a combination* is obtained by applying the procedure specified by the operator to the arguments that are the values of the operands.
	
- Lisp combinations use **prefix notation (the operator comes first)**
	- Prefix form can have arbitrary number of arguments.
	 ```Scheme
	  (+ 21 21 12 10 39) ;  5 arguments
	  (+ 11 23) ; 2 arguments
```

- Combinations can be nested.
	- An operator or an operand can be itself another combination.
	 ```Scheme
	 (+ (* 3 4) (- 10 5)) ; 17
```

	- A way to write nested expressions is to align the operands of the combinations vertically. This is known as *pretty printing*
	 ```Scheme
(+ (* 3
      (+ (* 2 4)
         (+ 3 5)))
   (+ (- 10 7)
      6))
```
	

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
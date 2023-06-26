---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #substitution_model_for_procedure_application, #sicp/ch1 

# The Substitution Model for Procedure Application

- What is substitution model?
	- To apply a compound procedure to *arguments*, evaluate the body of the procedure with each formal parameter replaced by the corresponding argument.
- Here is a compound procedure:
```Scheme
(define (f x) (sum-of-squares (+ x 1) (* x 2)))
```
- Here is the substitution model in work at the procedure application:
```Scheme
(f 5)
(sum-of-squares (+ 5 1) (* 5 2))
(sum-of-squares 6 10)
(+ (square 6) (square 10))
(+ (* 6 6) (* 10 10))
(+ 36 100)
136
```

## Applicative order vs Normal order
 - The example above used *applicative order*:  all sub-expressions are evaluated first, then applied the procedure to the arguments. 
	 - (+ 5 1 ) evaluated to 6 then square is applied to 6.
	 - Motto is  **"evaluate and then apply"**
	 
 - With *normal order*, operands are substituted in the procedure **unevaluated**. Only when it reaches primitive operators, we start reducing the combinations to values.
	 - Motto is **"fully expand and then reduce"**
 ```Scheme
 (f 5)
 (sum-of-squares (+ 5 1) (* 5 2))
 (+ (square (+ 5 1) (square (* 5 2))))
 (+ (* (+ 5 1 ) (+ 5 1)) (* (* 5 2) (* 5 2)))
 (+ (*  6 6) (* 10 10))
 (+ 36 100)
 136
```
   -  Pay  attention, normal order causes some combinations to be evaluated multiple times
	   - (+ 5 1) evaluated 2 times.

---

## 🔑 Key Points
- 
## ❓ Questions
- what is the difference between arguments(actual parameters) and formal parameters?
	-  The values that are declared within a function when the compound procedure is called are known as an argument.
	- Whereas, the variables that are defined when the compound procedure is declared are known as a parameters
- Is this substitution model simple? Do the interpreters really work this way using the textual replacement?
	- No, this is just a way of making it close how you think.
	- Why do we do it that way then?
		-  In general, when modeling an phenomena in science and engineering, we begin with simplified, incomplete models.
		- As we examine things in greater detail, these simple models become inadequate and must be replaced by more refined models
## 📦 Resources
-  [SICPE 1.05](./SICPE%201.05.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
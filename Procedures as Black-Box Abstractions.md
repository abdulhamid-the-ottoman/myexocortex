---
share: true
---
up:: [The Elements of Programming](./The%20Elements%20of%20Programming.md)
tags:: #procedures_as_blackbox_abstraactions #sicp/ch1 

# Procedures as Black-Box Abstractions

> [!INFO] The Gist
> A user should not need to know how the procedure is implemented in order to use it

- Each procedure in a program should accomplish an identifiable task that can be used as a module in defining other procedures.
- When we use a procedure as a  *"black box"*, **we are concerned with what it is doing but not how it is doing.**
	- This is called **procedural abstraction**, its purpose is to suppress detail.
- Here when we say procedural abstraction of square, we only know what it does, which is taking square of a number, but we have no idea how it is implemented:
```Scheme
(define (square x) (* x x))
(define (square x) (exp (double (log x))))
(define (double x) (+ x x))
```

## Local Names
- The choice of names for the procedure's formal parameters should not matter to the user of the procedure.
```Scheme
(define (square x) (* x x))
(define (square y) (* y y))
```
- Consequentially, the parameter names must be local to the body of the procedure.
- The name of a formal parameter doesn't matter; it is a *bound variable*. The procedure binds its formal parameters.
- If a variable is not bound, it is *free*.
- The (set of) expression(s) in which a binding exists is called *the scope* of the name. For parameters of a procedure, this is the body. Think of body as huge block expression.
- Look at the example below, guess and x are bound variables but < , abs, and square are free!.  The meaning of good-enough? is independent of the names we choose for guess and x so long as they are distinct from <, - , abs and square.
```Scheme
(define (good-enough? guess x)
  (< (abs (- (square guess) x)) 0.001))
```
- Using the same name for a bound variable and an existing free variable is called *capturing the variable*.
	- if we have renamed guess to abs, we would have introduced a bug by capturing the variable abs. - abs would become no longer free!
- The names of the free variables do matter for the meaning of the procedure.

## Internal definitions and block structure

- Putting a definition in the body of a procedure makes it local to that procedure. This nesting is called *block structure*.
	- this is the simplest solution to **name-packaging problem.**
- Now we have 2 kinds of *name isolation*: 
	- formal parameters
	- internal definitions.
- By internalizing auxiliary procedures, we can often eliminate bindings by allowing variables to remain free.
- Scheme uses *lexical scoping*, meaning free variables in a procedure refer to bindings in enclosing procedure definitions.

- Here is an example where we use block structure to simplify the code we have written. pay attention how x is a free variable for good-enough?, improve but a captured variable for average and square procedures.

```Scheme
#lang sicp

(define (sqrt x)
  (define (good-enough? guess)
    (< (abs (- (square guess) x)) 0.001))

  (define (improve guess)
    (average guess (/ x guess)))

  (define (average x y)
    (/ (+ x y) 2))

  (define (sqrt-iter guess)
    (if (good-enough? guess)
        guess
        (sqrt-iter (improve guess))))

  (define (square x)
    (* x x))
  
  (sqrt-iter 1.0))
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
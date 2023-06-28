---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #conditional_expressions_and_predicates #sicp/ch1 

# Conditional Expressions and Predicates

- To make more useful procedures, we need to be able to conduct tests and perform different operations accordingly.

- We do *case analysis* in Scheme using  <mark style="background: #FFB86CA6;">cond</mark> keyword
```Scheme
(cond (<p1> <e1>)
	  (<p2> <e2>)
	  ...
	  (<pn> <en>))
```

- The following form is called a *clause* and it is composed of a *predicate* represented with p and a *consequent* represented with c.

```Scheme
(<p> <c>)
```

- *Predicate* is an expression or procedure whose value is interpreted as either true or false.
	- Primitive predicates are <, > , =
- *A consequent* is an expression which follows the predicate.

- <mark style="background: #FFB86CA6;">cond</mark> expressions work by testing each predicate. The consequent expression of the first clause with a true predicate is returned, and other clauses are ignored.
	- The symbol <mark style="background: #FFB86CA6;">else</mark> can be used as the last clause, - it will always evaluate to true.

```Scheme
(define (abs x)
	(cond ((> x 0) x)
		  ((= x 0) 0)
		  (else (- x))))
```

- <mark style="background: #FFB86CA6;">if</mark> keyword can be used when there are only 2 cases and its general form is as follows:

```Scheme
(if <predicate> <consequent> <alternative>)
```

- Here is the same example using if:
```Scheme
(define (abs x)
  (if (< x 0) ; predicate
	  (-x) ; consequent
	  x ; alternative
	  ))
```

- Logical values can be combined with <mark style="background: #FFB86CA6;">and</mark>, <mark style="background: #FFB86CA6;">or</mark> and <mark style="background: #D2B3FFA6;">not</mark>. The first two (shown in orange) are special forms, not procedures, because they have short-circuiting behavior:

```Scheme
(and <e1> ... <en>) ; evals left to right, if e1 is false, no need to eval the rest
(or <e1> ... <en>) ; evals left to right, if e1 is true, no need to eval the rest
(not <e>)
```

---

## 🔑 Key Points
- 
## ❓ Questions
- What are the differences between cond and if?
	- consequent part of cond may be a sequence of expressions.
	- consequent and alternative parts of an if must be single expression.
- What are the true and false values in Scheme?
	- In scheme, there are 2 distinguished values that are denoted by constants  \#t  (true) and \#f (false).
	- When the interpreter checks a predicate's value, it interprets \#f as false, any other value is treated as true. (So \#t is unnecessary, but it is convenient)
## 📦 Resources
-  [Exercise 1](./SICPE%201.01.md)
- [ Exercise 2](./SICPE%201.02.md)
- [ Exercise 3](SICPE%201.03.md)
-  [Exercise 4](./SICPE%201.04.md)
-  [Exercise 5](./SICPE%201.05.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
---
created: ["2023-06-12 10:42"]
share: true
---

up::

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Alyssa P. Hacker doesn’t see why if needs to be provided as a special form. “Why can’t I just define it as an ordinary procedure in terms of cond?” she asks. Alyssa’s friend Eva Lu Ator claims this can indeed be done, and she defines a new version of if:
> 
> ```scheme
> (define (new-if predicate
>                 then-clause
>                 else-clause)
>   (cond (predicate then-clause)
>         (else else-clause)))
> ```
> Eva demonstrates the program for Alyssa:
> 
> ```scheme
> (new-if (= 2 3) 0 5)
> 5
> 
> (new-if (= 1 1) 0 5)
> 0
> ```
> Delighted, Alyssa uses new-if to rewrite the square-root program:
> ```scheme
> (define (sqrt-iter guess x)
>   (new-if (good-enough? guess x)
>           guess
>           (sqrt-iter (improve guess x) x)))
> ```
> What happens when Alyssa attempts to use this to compute square roots? Explain.


## 🔑 **Key Points of Understanding**

# 🔍 Solutions
- Since `new-if` is a function, and not a special form, each parameter subexpression will be evaluated _before_ the procedure is applied. It means that when evaluating:

```scheme
(new-if (good-enough? guess x)
      guess
      (sqrt-iter (improve guess x) x))
```

- the predicate and the two alternatives (consequent and alternative) will always be evaluated.
- Since the second alternative is calling the function itself in a recursive way, the function will be stuck in an infinite loop.
# 🧠 Ideas about Problem

# 🔗 Related Applications


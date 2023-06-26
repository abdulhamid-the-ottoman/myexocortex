---
created: ["2023-06-12 07:48"]
share: true
---

up::

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Observe that our model of evaluation allows for combinations whose operators are compound expressions. Use this observation to describe the behavior of the following procedure:
> ```scheme
(define (a-plus-abs-b a b)
  ((if (> b 0) + -) a b))

## 🔑 **Key Points of Understanding**

# 🔍 Solutions
- if b is positive, the operator expression shown below will evaluate to +, then the result is a+b, and in all other cases, it will evaluate to - , then the result will be a - b.
```Scheme
(if (> b 0) + -)
```
# 🧠 Ideas about Problem

# 🔗 Related Applications


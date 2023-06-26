---
created: ["2023-06-14 20:09"]
share: true
---

up::

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> - A function f is defined by the rule that 
> 	- f(n)=n if n<3 and
> 	- f(n)=f(n−1)+2f(n−2)+3f(n−3) if n≥3.
> - Write a procedure that computes f by means of a recursive process. Write a procedure that computes f by means of an iterative process.

## 🔑 **Key Points of Understanding**

# 🔍 Solutions
- Iterative process:
```Scheme
#lang sicp

(define (f n)
  (f-iter 2 1 0 (- n 2)))

(define (f-iter n2 n1 n0 cnt)
  (if (= cnt 0)
      n2
      (f-iter (+ n2 (* 2 n1) (* 3 n0))
              n2
              n1
              (- cnt 1))))

(f 3) ; 4
(f 4) ; 11
(f 5) ; 25
(f 6) ; 59
```

- Here is an trace for (f 6)
```Scheme
>(f-iter 2 1 0 4)
>; 1 st iteration
>(f-iter 4 2 1 3)
>; 2 nd iteration
>(f-iter 11 4 2 2)
>; 3 rd iteration
>(f-iter 25 11 4 1)
>; 4 th iteration
>(f-iter 59 25 11 0)
<59
59
```

- Recursive process:
```Scheme
(define (fr n)
  (if (< n 3)
      n
      (+ (fr (- n 1)) (* 2 (fr (- n 2))) (* 3 (fr (- n 3))))))

(f 3) ; 4
(f 4) ; 11
(f 5) ; 25
(f 6) ; 69
```

- Here is the trace for (fr 5) - the recursive process
```Scheme
>(fr 5)
> (fr 4)
> >(fr 3)
> > (fr 2)
< < 2
> > (fr 1)
< < 1
> > (fr 0)
< < 0
< <4
> >(fr 2)
< <2
> >(fr 1)
< <1
< 11
> (fr 3)
> >(fr 2)
< <2
> >(fr 1)
< <1
> >(fr 0)
< <0
< 4
> (fr 2)
< 2
<25
25
> 
```

- Here is the tree - recursion visually:
![Pasted image 20230615102646.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230615102646.png)

# 🧠 Ideas about Problem

# 🔗 Related Applications


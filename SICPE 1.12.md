---
created: ["2023-06-15 10:30"]
share: true
---

up::[SICP-Chapter1-Exercises](./SICP-Chapter1-Exercises.md)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> - The following pattern of numbers is called Pascal’s triangle.
> 
> ```
>          1
>        1   1
>      1   2   1
>    1   3   3   1
>  1   4   6   4   1
>        . . .
> ```
> 
> - The numbers at the edge of the triangle are all 1, and each number inside the triangle is the sum of the two numbers above it. Write a procedure that computes elements of Pascal’s triangle by means of a recursive process.


## 🔑 **Key Points of Understanding**
- First design a procedure to print an element at specific row and index -- pte procedure
	- level -> row
	- i -> col
- Then design a procedure to print out a specific row -- drow
	- In order to print all the elements at that level --> you have to define an iterative process, which we did by print-elem-iter
- Then design a procedure to print out the whole triangle - dpt

- Printing out to the console is done with display procedure 
	- First time using it.
# 🔍 Solutions

```Scheme
#lang sicp
;#lang racket
;(require racket/trace)

;display pascal triangle element
(define (pte l i)
  (if (or (= i 1) (= l i))
      1
      (+ (pte (- l 1) (- i 1))
         (pte (- l 1) i))))

;dpt - display pascal triangle
(define (dpt l)
  (define (dpt-iter cnt)
    (cond ((> cnt l) (display "\n"))
          (else (drow cnt)
                (dpt-iter (+ cnt 1)))))
  (dpt-iter 1)
  )

;display row
(define (drow level)
  (define (print-elem-iter i level)
    (cond ((> i level) (display "\n"))
          (else (display (pte level i))
                (display "  ")
                (print-elem-iter (+ i 1) level))))
  (print-elem-iter 1 level)
  )

(dpt 15)
```

- Here is the result:
```Scheme
1  
1  1  
1  2  1  
1  3  3  1  
1  4  6  4  1  
1  5  10  10  5  1  
1  6  15  20  15  6  1  
1  7  21  35  35  21  7  1  
1  8  28  56  70  56  28  8  1  
1  9  36  84  126  126  84  36  9  1  
1  10  45  120  210  252  210  120  45  10  1  
1  11  55  165  330  462  462  330  165  55  11  1  
1  12  66  220  495  792  924  792  495  220  66  12  1  
1  13  78  286  715  1287  1716  1716  1287  715  286  78  13  1  
1  14  91  364  1001  2002  3003  3432  3003  2002  1001  364  91  14  1  
```

- Here is the trace of pte function in (dpt 3)

```Scheme
Triangle:
1  
1  1  
1  2  1  

Trace:
>(pte 1 1)
<1
1  
>(pte 2 1)
<1
1  >(pte 2 2)
<1
1  
>(pte 3 1)
<1
1  >(pte 3 2)
> (pte 2 1)
< 1
> (pte 2 2)
< 1
<2
2  >(pte 3 3)
<1
1  
```
- Pay attention how (pte 3 2) calls (pte 2 1) and (pte 2 2)
# 🧠 Ideas about Problem

# 🔗 Related Applications


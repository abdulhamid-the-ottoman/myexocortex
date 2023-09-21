---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #exponentiation, #sicp/ch1 

# Exponentiation
- One way to calculate b to the $n^{th}$ power is via the following recursive definition:
		![300](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230614164433.png)
	 - Here is the code:

```Scheme
#lang sicp
(define (pow b n)
  (if (= n 0)
      1
      (* b (pow b (- n 1)))))

(pow 2 5)
```

- A faster method is to use successive squaring:
		![300](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230614164336.png)
	 - Here is the code:
```Scheme
#lang sicp

(define (pow b n)
  (cond ((= n 0) 1)
        ((even? n) (square (pow b (/ n 2))))
        (else (* b (pow b (- n 1))))
        ))

(define (square n)
  (* n n))

(define (even? x)
  (= (remainder x 2) 0))

(pow 2 5)
```

---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [Exercise 16](./SICPE%201.16.md)
- [Exercise 17](Exercise%201.17.md)
- [Exercise 18](Exercise%201.18.md)
- [Exercise 19](Exercise%201.19.md)

## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
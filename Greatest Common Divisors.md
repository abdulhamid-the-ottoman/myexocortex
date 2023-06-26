---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #gcd #sicp/ch1 

# Greatest Common Divisors
- The GCD of integers a and b is the largest integer that divides both a and b with no remainder. 
	- For example, gcd(16,28) = 4.
- An efficient algorithm uses gcd(a,b) = gcd(b, a mod b)
- Here is an example:

> [!INFO] GCD TRACE
>(gcd 206 40)
>(gcd 40 6)
>(gcd 6 4)
>(gcd 2 0)
>2

- This always works: you always get a pair where the second number is zero, and the other number is the GCD of the original pair.
	- This is called Euclid's Algorithm
- Here is the scheme implementation:
```Scheme
(define (gcd a b)
  (if (= b 0)
      a
      (gcd b (remainder a b)))
  )

(gcd 206 40)
```

- Lame's Theorem: If Euclid's Algorithm requires k steps to compute the GCD of some pair (a,b), then min{a,b} >= Fib(k).

---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [Exercise 1.20](Exercise%201.20.md) 
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
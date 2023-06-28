---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #testing_for_primality, #probabilistic_methods #sicp/ch1 

# Testing for Primality
## Searching for divisors
- One way to test for primality is to find the number's divisors
- A number is prime if and only if it is its own smallest divisor.

## The Fermat test
- The Fermat test is a $\theta(log(n))$ primality test based on Fermat's Little Theorem:

> [!INFO] The Main Idea
> - If *p* is a prime number and *a* is any positive integer less than p, then a raised to the *$p^{th}$*  power is congruent to *a modulo p*.
> - $a^p$ $\equiv$ a mod p

- The test works as follows:
	- Given a number p (the number we are testing its primality), pick a random number a < n and calculate $a^p$ mod p
	- **Fail:** If the result is not equal to a, then n is not prime.
	- **Pass:** If the result is equal to a , then n is likely a prime
	- **Repeat :** The more times the number passes the test, the more confident we are that n is prime. If there is a single failure, n is certainly not a prime.

## Probabilistic Methods
- Most familiar algorithms compute an answer that is guaranteed to be correct.
- Not so with the Fermat test. If n passes the Fermat test for one random value of a, all we know is that there is a better than 50% chance of n being prime
- A probabilistic algorithm doesn't always give a correct result, but you can prove that the chance of error becomes arbitrarily small.
- We can make the probability error in our primality test as small as we like by simply running more Fermat tests - except Carmichael numbers.

> [!INFO] Carmichael Numbers
> - Numbers that fool the Fermat test are called Carmichael numbers.
> - Little is known about them other than that they are extremely rare.
> - In testing primality of very large numbers chosen at random, the chance of stumbling upon a value that fools the Fermat test is less than the chance that cosmic radiation will cause the computer to make an error in carrying out a "correct" algorithm.
> - Considering this algorithm to be inadequate for the reason that there are Carmichael numbers, but adequate because the chance of stumbling on such a number is very small is exactly the difference between mathematics and engineering.

---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [Exercise 21](SICPE%201.21.md)
- [Exercise 22](SICPE%201.22.md)
- [Exercise 23](SICPE%201.23.md)
- [Exercise 24](SICPE%201.24.md)
- [Exercise 25](SICPE%201.25.md)
- [Exercise 26](SICPE%201.26.md)
- [Exercise 27](SICPE%201.27.md)
- [Exercise 28](SICPE%201.28.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
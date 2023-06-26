---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #orders_of_growth, #sicp/ch1 

# Orders of Growth
- Different processes consume different amounts of computational resources
- We compare this using *order of growth*, a crude measure of the resources required by a process as the inputs become larger.
- Let n be a parameter that measures the size of a problem - it could be the input itself, the tolerance, the number of rows in the matrix, etc.
- Let R(n) be the amount of resources the process requires for a problem of size n. This could be time, space(amount of memory), number of registers used , etc.
- We say that R(n) has order of growth $\theta(f(n))$, or $R(n) = \theta(f(n))$, meaning if there are positive constants A and B independent of n such that A.f(n) < R(n) < B.f(n) for any sufficiently large value of n.
- The value R(n) is sandwiched between A.f(n) and B.f(n)
- The linear recursive process for computing factorials had $\theta(n)$ time and $\theta(n)$ space (both linear), whereas the linear iterative process had $\theta(1)$ space (constant).
- The tree recursive Fibonacci computation requires $\theta(\phi^{n})$ steps and space $\theta(n)$ space where $\phi$ is the golden ratio.
- The order of growth is a crude description of the behavior of a process.
- Its importance is allowing us to see the change in the amount of resources required when you, say, increment n or double n.
---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [SICPE 1.14](./SICPE%201.14.md)
- [SICPE 1.15](./SICPE%201.15.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
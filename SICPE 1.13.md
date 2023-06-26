---
created: ["2023-06-15 11:57"]
share: true
---

up::

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
>- Prove that Fib(n) is the closest integer to $φ^n$/√5, where φ=(1+√5)/2. Hint: Let ψ=(1−√5)/2. Use induction and the definition of the Fibonacci numbers (see 1.2.2) to prove that Fib(n)=($φ^n$−$ψ^n$)/√5.

## 🔑 **Key Points of Understanding**

# 🔍 Solutions
- The constants φ and ψ are the solutions to golden ratio equation x + 1 = $x^2$:
	- In an equation like a$x^2$ + bx + c = 0:
		- $\Delta$ = $b^2$ - 4ac
		-  φ = $\frac{-b + \sqrt{\Delta}}{2a}$
		-  ψ =  $\frac{-b - \sqrt{\Delta}}{2a}$
	- In our case :
		- φ = $\frac{1 + \sqrt{5}}{2}$
		- ψ = $\frac{1 - \sqrt{5}}{2}$
- The fibonacci sequence is defined recursively by
	- Fib(0) = 0
	- Fib(1) = 1
	- Fib(n) = Fib(n-1) + Fib(n-2)

- Lemma : Fib(n) is equal to f(n) = $\frac{φ^n - ψ^n}{\sqrt{5}}$

- Proof:
	- Let's demonstrate 3 base cases. 
		- When n = 0,  f(0) =  $\frac{φ^0 - ψ^0}{\sqrt{5}}$ =  $\frac{1 - 1}{\sqrt{5}}$ = 0
		- When n = 1,   f(1)  =  $\frac{φ^1 - ψ^1}{\sqrt{5}}$ = $\frac{\frac{1 + \sqrt{5}}{2} + \frac{1 - \sqrt{5}}{2}}{\sqrt{5}}$ = $\frac{\frac{2\sqrt{5}}{2}}{\sqrt{5}}$ = 1.
		- When n = 2,  f(2) =  $\frac{φ^2 - ψ^2}{\sqrt{5}}$ = 1
		
	- Now comes the inductive step:
		![400](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230615121806.png)
		 - One thing you have to realize from above is (1 + $φ^{-1}$) = φ or (1+$ψ^{-1}$) = ψ 
	 - By induction, f(n) = Fib(n) for all n.
	 
- Theorem Fib(n) is closest integer to $\frac{φ^n}{\sqrt{5}}$ where φ = $\frac{1 + \sqrt{5}}{2}$
	- Proof: It suffices to show that absolute difference is less than one half:
		![400](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230615123015.png)
	- Since |ψ| < 0.619 < 1, we have $|ψ|^{n}$ < 1 < $\frac{\sqrt{5}}{2}$

# 🧠 Ideas about Problem

# 🔗 Related Applications


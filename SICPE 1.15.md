---
created: ["2023-06-15 15:57"]
share: true
---

up::

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> - The sine of an angle (specified in radians) can be computed by making use of the approximation sinx≈x if x is sufficiently small, and the trigonometric identity
> 
>	- sin x = 3 sin $\frac{x}{3}$ - 4$sin^3 \frac{x}{3}$
> 
> - to reduce the size of the argument of sin. (For purposes of this exercise an angle is considered “sufficiently small” if its magnitude is not greater than 0.1 radians.) These ideas are incorporated in the following procedures:
> 
> ```scheme
> (define (cube x) (* x x x))
> (define (p x) (- (* 3 x) (* 4 (cube x))))
> (define (sine angle)
>    (if (not (> (abs angle) 0.1))
>        angle
>        (p (sine (/ angle 3.0)))))
> ```
> 
> 1. How many times is the procedure `p` applied when `(sine 12.15)` is evaluated?
> 2. What is the order of growth in space and number of steps (as a function of `a`) used by the process generated by the sine procedure when `(sine a)` is evaluated?

## 🔑 **Key Points of Understanding**

# 🔍 Solutions

#### How many time is p evaluated.
- The execution trace from Dr Racket:
```Scheme
>(sine 12.5)
> (sine 4.166666666666667)
> >(sine 1.388888888888889)
> > (sine 0.462962962962963)
> > >(sine 0.154320987654321)
> > > (sine 0.051440329218107005)
< < < 0.051440329218107005
> > >(p 0.051440329218107005) ;; 1
< < <0.153776521096694
> > (p 0.153776521096694) ;; 2
< < 0.4467840153484446
> >(p 0.4467840153484446) ;; 3
< <0.9836111719853284
> (p 0.9836111719853284) ;; 4
< -0.8557060643295382
>(p -0.8557060643295382) ;; 5
<-0.060813768577286265
-0.060813768577286265
```

- If you trace it by hand:
```Scheme
(sine 12.15) 
	~> (p (sine 4.05)) 
		~> (p (p (sine 1.35))) 
			~> (p (p (p (sine 0.45)))) 
				~> (p (p (p (p (sine 0.15))))) 
					~> (p (p (p (p (p (sine 0.05)))))) ; five times until theta <= 0.1
```

#### Growth of space & steps
- During the process, the p is evaluated k times such that $a / 3^k$ < 0.1. Solving for k gives
	- $a / 0.1$ < $3^k$  and we take the $log_3$ of both sides
	- $log_3 10a$ < k, thus the number of steps for sine grows as $\Theta(log a)$
- The interpreter must maintain the stack for that number of calls to p, so the space complexity is also $\Theta(log a)$
# 🧠 Ideas about Problem

# 🔗 Related Applications


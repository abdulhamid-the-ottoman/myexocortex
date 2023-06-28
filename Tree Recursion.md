---
share: true
---
up:: [Building Abstractions with Procedures](./Building%20Abstractions%20with%20Procedures.md)
tags:: #tree_recursion , #factorial_example, #coin_change_example

# Tree Recursion
- With tree recursion, the procedure invokes itself more than once, causing the process to evolve in the shape of a tree.
- The naive fibonacci procedure calls itself twice each time it is invoked, so each branch splits into two at each level.

>[!INFO] The Gist
>In general, the number of steps required by a tree-recursive process will be proportional to the number of nodes in the tree, while the space required will be proportional to the maximum depth of the tree.

#### The Factorial Example
- The mathematical function is defined as follows:
![Pasted image 20230614112219.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230614112219.png)

- The scheme code as a recursive procedure:
```Scheme
(define (fib n)
  (cond ((= n 0) 0)
        ((= n 1) 1)
        (else (+ (fib (- n 1)) 
			     (fib (- n 2))))))
```

- The tree it constructs:
![Pasted image 20230614113125.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230614113125.png)
- Pay attention that fib 3 constitutes almost half of the computation and it is computed twice (lots of redundant computation) 
- In fact Fib(n) grows exponentially with n. More precisely Fib(n) is closes to integer $\phi / \sqrt{5}$ where $\phi = \frac{1+\sqrt{5}}{2} \simeq 1.6180$
		- $\phi$ is also called the *golden ratio* and given by the equation $\phi ^{2}  = \phi +1$
		- Thus the process uses a number of steps that *grows exponentially* with the input.
		- The space required *grows only linearly* with the input, because we need keep track only of the nodes are above us in the tree at any point in the computation.

- Here is an  implementation generating an iterative process which holds 4 variables for state.
```Scheme
(define (fib n)
  (fib-iter 1 0 1 n))

(define (fib-iter total prev cnt num)
  (if (= cnt num)
      total
      (fib-iter (+ total prev) total (+ cnt 1) num)))
```

- Here is a trace of (fib 3)

```Scheme
>(fib-iter 1 0 1 3) ; 1st call
>;first iteration  - (1+0)
>(fib-iter 1 1 2 3) ; 2nd call
>;second iteration - (1+1)
>(fib-iter 2 1 3 3) ; 3rd call
<2
2
```

- Here another  implementation generating an iterative process which holds 3 variables for the state.
```Scheme
(define (fib n)
  (fib-iter 1 0 n))

(define (fib-iter a b cnt)
  (if (= cnt 0)
      b
      (fib-iter (+ a b) a (- cnt 1))))
```
- Here is a trace while executing (fib 3)
```Scheme
>(fib-iter 1 0 3) ; 1st call
>;first iteration  - (1+0)
>(fib-iter 1 1 2) ; 2nd call
>;second iteration - (1+1)
>(fib-iter 2 1 1) ; 3rd call
>;third iteration  - (1+2)
>(fib-iter 3 2 0) ; 4th call
<2
2
```
- We can also implement the same in a language like C++
```C++
int fib(int n){
  int b = 0;
  int a = 1;
  for(int i = 0; i<n ; ++i){ // n=3 iterations! (n=3 additions)
	  int sum = a + b;
	  b = a;
	  a = sum;
  }
  return b;
}
```

#### Example: Counting Change

^cdcde0
- Let f(A,N) represent the number of ways of changing the amount A using N kinds of coins.
- If the first kind of coin has denomination D, then f(A,N) = f(A, N-1) + f(A-D,N)
	- In other words, there are 2 situations : where you don't use any of the first kind of coin, and when you do.
	- f(A,N-1) assumes we don't use the first kind at all.
	- f(A-D, N) assumes we use all kinds of coins after we used the first one as D.
- That rule and a few degenerate cases are sufficient to describe an algorithm for counting the number of ways of changing amounts of money. We can define it with the following piecewise function:
		![500](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230614120525.png)
- Like fibonacci, the easy tree-recursive implementation involves a lot redundancy.
	- Unlike fibonacci, there is no obvious iterative solution (it is possible, just harder).
	- One way to get rid of redundant computations and improve the performance of the tree-recursive process is to use *memoization*
	- memoization means put the result in a table and access it instead of recomputing.

- Lets have a real life example of this : 
	- you have 50 TRY, and you want to use 20 TRY ->1st type of denomination and 10 TRY->2nd type of denomination to change it.
	- f(50,{20,10}) -> means the number of ways 50 try can be changed in terms of 20 and 10 try
	- f(50,{20,10}) = f(50,{10}) + f(30,{20,10})
		- f(50,{10}) is equal to 1 because there is only **{10,10,10,10,10}**
		- f(30,{20,10}) = f(30,{10}) + f(10,{20,10})
			- f(30,{10}) is equal to 1, because there is only {10,10,10} ->  but in terms of total change it is **{20,10,10,10}** , because we used the first denomination as 20.
			- f(10,{20,10}) = f(10,{10}) + f(-10,{20,10})
				- f(10,{10}) is equal to 1 , because there is only {10} -> but in terms of total change it is **{20,20,10}**
				- f(-10,{20,10}) is equal to 0, because negative money doesn't exist.
	 - Here is the computation tree:
	 ![Pasted image 20230614131312.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230614131312.png)
- Lets write the code of it:
```Scheme
#lang sicp

(define (cc amt k)
  (cond ((= amt 0) 1)
        ((or (< amt 0) (= k 0)) 0)
        (else (+ (cc amt (- k 1))
                 (cc (- amt (select k)) k)))))

(define (select k)
  (cond ((= k 1) 20)
        ((= k 2) 10)))


(cc 50 2)
```
---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [Exercise 11](./SICPE%201.11.md)
- [Exercise 12](./SICPE%201.12.md)
- [Exercise 13](./SICPE%201.13.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
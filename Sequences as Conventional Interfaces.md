---
share: true
---

up:: [Building Abstractions With Data](./SICP.md#^d1c4f8)
tags::  #map #mapcat #sequences

# Sequences as Conventional Interfaces
- Abstractions preserves the flexibility to experiment with alternative representations
- To use of *conventional interfaces* is another powerful design principle
- To make abstract operations for things other than numbers, we need to have a conventional style in which we manipulate data.
- Here is a procedure which takes a tree as argument and computes the sum of the squares of the leaves that are odd:
```Scheme
#lang sicp

(define (square a)
  (* a a))

(define (sum-odd-squares tree)
  (cond ((null? tree) 0)
        ((not (pair? tree)) (if (odd? tree)
                                (square tree)
                                0))
         (else (+ (sum-odd-squares (car tree))
                  (sum-odd-squares (cdr tree))))))
```

- This program
	- enumerates the leaves of a tree
	- filters them, selecting the odd ones
	- squares each of the selected ones
	- accumulates the results using +, starting with 0.
	 ![Pasted image 20230731101650.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230731101650.png)

	- We begin with an enumerator which generates a *signal* consisting of the leaves of given tree.
	- The signal is passed through a *filter* , which eliminates all but the odd elements
	- The resulting signal is in turned passed through a **map**, which is a *transducer* that applies the square procedure to each element.
		-  a transducer converts a signal in one form of energy to a signal in another.
	- The output of the map is then fed to an *accumulator*, which combines the elements using +, starting from an initial 0.

- Or here is a piece of code which constructs a list of all the even Fibonacci numbers Fib(k), where k is less than or equal to a given integer n:
```Scheme
(define (fib n)
  (if (< n 2)
      n
      (+ (fib (- n 1))
         (fib (- n 2)))))
  

(define (even-fibs n)
  (define (next k)
    (if (> k n)
        nil
        (let ((f (fib k)))
          (if (even? f)
              (cons f (next (+ k 1)))
              (next (+ k 1))))))
  (next 0))

  (even-fibs 10)
  > (0 2 8 34)
```

- This program
	- enumerates the integers from 0 to n
	- computes the Fibonacci number for each integer
	- filters them, selecting the even ones
	- accumulates the results using cons, starting with the empty list.
	 ![Pasted image 20230731101849.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230731101849.png)
	- This is also analogous as for the plan
## Sequence operations

^99215e

- We want to organize programs to reflect *signal-flow* structure. 
	- The two procedure definitions above fail to exhibit this signal-flow structure.
		- in sum-odd-squares, we find that the enumeration is implemented partly by null? and pair? tests and partly by the tree recursive structure of the procedure.
		- Similarly, the accumulation is found partly in tests and partly in the addition used in the recursion.
	- In general, there are no distinct parts of either procedure correspond to elements in the signal-flow description
		- There is no conceptual clarity, they spread the enumeration over the program and mingle it with map, the filter and the accumulation.
- To do this, 
	- We focus on the signals and represent them as lists
	- We can use list operations to implement the processing at each of the stages.
	- For example
		- we can implement the mapping stages of the signal flow diagrams using the map procedure
		- `(map square (list 1 2 3 4 5))`
		- `>(1 4 9 16 25)`
	- Filtering a sequence to select only those elements that satisfy a given predicate is accomplished by
	```Scheme
(define (filter predicate sequence)
  (cond ((null? sequence) nil)
        ((predicate (car sequence)) (cons (car sequence)
                                          (filter predicate (cdr sequence))))
        (else (filter predicate (cdr sequence)))))
(filter odd? (list 1 2 3 4 5))
> (1 3 5)
```

	- Accumulation can be implemented as
```Scheme
(define (accumulate op initial sequence)
  (if (null? sequence)
      initial
      (op (car sequence)
          (accumulate op initial (cdr sequence)))))
(accumulate + 0 (list 1 2 3 4 5)) 
> 15
(accumulate * 1 (list 1 2 3 4 5))
> 120
(accumulate cons nil (list 1 2 3 4 5))
>(1 2 3 4 5)
```

- Now we can reformulate sum-odd-squares and even-fibs as in the signal-flow diagrams
```Scheme
(define (emumerate tree)
  (cond ((null? tree) nil)
        ((not (pair? tree)) tree)
        (else (append (enumerate (car tree))
                      (enumerate (cdr tree))))))

>(enumerate (list 1 (list 2 (list 3 4)) 5))
> (1 2 3 4 5)

(define (sum-odd-squares tree)
  (accumulate + 0 (map square (filter odd? (enumerate tree)))))
> (35)
```

- For even-fibs
```Scheme
(define (enumerate low high)
  (if (> low high)
      nil
      (cons low (enumerate (+ low 1) high))))
>(enumerate 2 7)
>(2 3 4 5 6 7)

(define (even-fibs n)
  (accumulate cons
              nil
              (filter even? (map fib (enumerate 0 n)))))
```

- Expressing programs as sequence operations helps us make program designs that are *modular* - made of relatively independent pieces that we can connect in flexible ways.
	- This is a strategy for controlling complexity.
- We can write a procedure which creates a list of fib squares
```Scheme
(define (list-fib-squares n)
  (accumulate cons nil (map square (map fib (enumerate 0 n)))))
```
- We can use these to calculate product of the squares of the odd integers in a sequence.
```Scheme
(define (product-of-squares-of-odds sequence)
  (accumulate * 1 (map square (filter odd? sequence))))
```
- A surprisingly vast range of operations can be expressed as sequence operations.
- Sequences, implemented here as lists, serve as a conventional interface that permits us to combine processing modules.
- Additionally, when we uniformly represent structures as sequences,
	- we have localized the data-structure dependencies in our programs to a small number of sequence operations.
	- By changing these, we can experiment with alternative representations of sequences, while leaving the overall design of our programs intact.

> [!INFO]  Data Abstraction
>  - One of the reasons for the success of Lisp as a programming language is that lists provide a standard medium for expressing ordered collections so that they can be manipulated using higher-order operations.
>  - The programming language APL owes much of its power and appeal to a similar choice.
> 	 - In APL, all data are represented as arrays, and there is a universal and convenient set of generic operators for all sorts of array operations

## Nested mappings

^38bc82
- For many computations, the sequence paradigm can be used instead of loops.
- Sometimes we need `nested mappings`, where each mapping maps to a second set of mappings.
- Consider this problem:
	- Given a positive integer n, find all ordered pairs of distinct positive integers i and j, where  `1 <= j < i <= n`, such that `i+j` is prime
- A natural way to organize this computation is to generate the sequence of all ordered pairs of positive integers less than or equal to n
	- filter to select those pairs whose sum is prime.
	- for each pair (i,j) that passes through the filter, produce the triple (i,j,i+j)
- We can enumerate all the integers as i which are smaller or equal to n
	- then generate all the integer as j which are smaller than i
	- filter it to select the ones whose sum is prime
	- then produce the triple

### Generating Power Sets
- Consider the problem of generating the power set of the set {1,2,3}
	- The power set is the set of all subsets
	- An arbitrary subset can elect to include or exclude each element.
- Here are the 8 sets making up the power set of {1,2,3}
	- {},{1},{2},{3},{1,2},{1,3},{2,3},{1,2,3}
	- They are topologically sorted from small to large.
- Power-sets has an inductive structure
	1. row :    {},{2},{3},{2,3}
	2. row : {1},{1,2},{1,3},{1,2,3}
	- The first row is the power-set of {2,3}
	- The second row is the power-set of {2,3} all over again, except that a 1 has been included in each one.
- There is our recursive structure
	- The power set of {1,2,3} is really 2 copies of {2,3}'s power set chained together, except that the second copy prepends a 1 onto the front of each entry.
- Here is the break down
	- The power set of {} is. {{}}.
		- That's because the empty set is a subset of itself.
	- The power-set of a non-empty set `A` with first element `a` is equal to the concatenation of two sets:
		- the first set is the power-set of A-{a}. This recursively gives us all those subsets of A that exclude a.
		- the second set is once again the power set of A-{a}, except that a has been prepended aka consed to the front of every subset.
- Here is the code
```Scheme
#lang sicp

(define (power-set set)
  (if (null? set)
      (list nil)
      (let ((power-set-except (power-set (cdr set))))
        (append power-set-except
                (map (lambda (p) (cons (car set) p))
                     power-set-except)))
  ))

(power-set `(1,2,3,4))

> (() (4) (3) (3 4) (2) (2 4) (2 3) (2 3 4) (1) (1 4) (1 3) (1 3 4) (1 2) (1 2 4) (1 2 3) (1 2 3 4))
```

- Note the use of a single `let` binding to preserve the value of the recursively generated power set.
	- It is because of the `let` statement that we reduce a doubly recursive implementation to a singly recursive one.
	- This actually reduced the running time of the algorithm quite a bit.
- The algorithm is particularly cool in Scheme because Scheme allows on-the-fly **lambda** to be implemented in terms of the `car` that was excluded from the recursive call.
	- That's how the second half is transformed from a set that excludes the first element to one that embraces it.


### Permutations
- Now consider the problem of generating all of the permutations of a list.
	- Let's start with a simple illustration by considering the permutations of {1,2,3,4}
		![Pasted image 20230727182537.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230727182537.png)
	- Notice that the first column includes all of those permutations that start off with a 1, and there are six of them.
	- The second column includes the permutations starting out with a 2, similarly for columns for three and four.
	- Each column has 3! = 6 permutations, because each places some number at the front of every permutation of the other three.
- What has been said so far can be framed in terms of mapping.
	- One significant component of the map is the transformation of each element into set of those permutations that begin with it.
	- The mapping routine needs to take an element and generate a list of permutations.
	 ![Pasted image 20230727183436.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230727183436.png)
- If there are 4 elements in the original list, there are 4 elements in the final list generated by any call to `map`
	- we can concat the 4 lists by `apply` ing `append` just prior to exit.
	- This means, we have a partial implementation, and it looks like this:
```Scheme
(define (permutations items)
  (if (null? items)
	  (list nil)
	  (apply append
		 (map <function to be determined> 
		      items))
  ))
```

- This mapping function isn't exactly trivial.
	- It needs to transform an isolated element into a list of permutations, where every permutation in that list begins with said element.
	- We can write it as a `lambda` function, which recognizes that its incoming argument is the element that needs to be at the front of all permutations it generates.
	- In order to generate those permutations, it must remove the element from the list recursively generate all of its permutations, and then map over that list so it can *cons* the distinguished element on to the front of each of its permutations.
```Scheme
(lambda (element)
	  (map <another-function-to-be-determined> (permutations (remove items element))))
```

- This inner mapping function is easier
	- it just needs to *cons* the incoming element to the front of each permutation produced by the recursive **permutations** call.
	- Assuming that *element* is in scope, **\<another-function-to-be-determined\>** can be replaced by:
```Scheme
(lambda (permutation)
		  (cons element permutation))
```

- Here is the full code:
```Scheme
(define (all-permutations items)
  (if (null? items)
      (list nil)
      (apply append (map (lambda (item)
             (map (lambda (permutation)
                    (cons item permutation))
                  (all-permutations (remove items item))))
           items))))

(define (remove ls elem)
  (cond ((null? ls) '())
        ((equal? (car ls) elem) (remove (cdr ls) elem))
        (else (cons (car ls) (remove (cdr ls) elem)))))

(all-permutations `(1,2,3))

> ((1 2 3) (1 3 2) (2 1 3) (2 3 1) (3 1 2) (3 2 1))
```

- Here is another version of the same code:
```Scheme
(define (all-permutations items)
  (if (null? items)
      (list nil)
      (apply append (map (gen-perms items) items))))

(define (gen-perms items)
  (lambda (item) (map (gen-prepender item)
                      (all-permutations (remove items item)))))

(define (gen-prepender item)
  (lambda (permutation) (cons item permutation)))


(define (remove ls elem)
  (cond ((null? ls) '())
        ((equal? (car ls) elem) (remove (cdr ls) elem))
        (else (cons (car ls) (remove (cdr ls) elem)))))

(all-permutations `(1,2,3))
> ((1 2 3) (1 3 2) (2 1 3) (2 3 1) (3 1 2) (3 2 1))
```
---

## 🔑 Key Points
- 
## ❓ Questions
- [ Sequence Operations](Sequences%20as%20Conventional%20Interfaces.md#^99215e)
	- [ Exercise 33 ](SICPE%202.33.md)
	- [ Exercise 34 ](SICPE%202.34.md)
	- [ Exercise 35 ](SICPE%202.35.md)
	- [ Exercise 36 ](SICPE%202.36.md)
	- [ Exercise 37 ](SICPE%202.37.md)
	- [ Exercise 38 ](SICPE%202.38.md)
	- [ Exercise 39 ](SICPE%202.39.md)
- [ Nested Mappings](Sequences%20as%20Conventional%20Interfaces.md#^38bc82)
	- [ Exercise 40 ](SICPE%202.40.md)
	- [ Exercise 41 ](SICPE%202.41.md)
	- [ Exercise 42 ](SICPE%202.42.md)
	- [ Exercise 43 ](SICPE%202.43.md)
## 📦 Resources
- 
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
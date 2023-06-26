---
share: true
---
up:: [SICP](./SICP.md)
tags:: #higher_order_procedures 

# Higher-Order Procedures
## Part 1
#### Don't repeat yourself
- So far Lisp might just seem like a different language with funny syntax. It's time to shatter that illusion.
- We are familiar with creating recursive procedures such as calculating the sum of integers from `a` to `b`.
- What about the sum of the squares of the squares of the integers from `a` to `b`?
	- That's almost the same program! and We don't like repetition.

> [!INFO] The Gist
>  - Now, whenever you see yourself writing the same thing down more than once, there is something wrong, and you shouldn't be doing it.
>  - And the reason is not because it's a waste of time to write something down more than once.
>  - It is increasing complexity. Now you end up remembering more than one thing. 
>  - To tame the complexity, and build complicated systems, and understand them,
> 	 - it is crucial to divide the things up into as many pieces as you can, each of which you can understand seperately.

- No repetition means you only write once, but also only understand and debug it once!
- Any time you see things that are almost identical, think of an abstraction to cover them.
- An idiom is a common pattern in a language that is useful to know. In Lisp, we can give idioms names and abstract them.
- There is nothing very special about numbers, Numbers are just one kind of data. Procedures are data as well.

#### Summation
- We can represent $\Sigma$ notation with a procedure that takes other procedures as arguments:
```Scheme
(define (sum term a next b)
  (if (> a b)
      0
      (+ (term a)
         (sum term (next a) next b))))
```

- Now we can write particular cases easily, without repeating ourselves:

```Scheme
(define (sum-int a b)
  (sum (lambda (x) x) a (lambda (x) (+ x 1 )) b))

(define (sum-sq a b)
  (sum (lambda (x) (* x x)) a (lambda (x) (+ x 1)) b))

(define (pi-sum a b)
  (sum (lambda (i) (/ i (* i (+ i 2))))
       a
       (lambda (i) (+ i 4))
       b))
```

 - We are separating the things we are adding up from the method of doing addition.
 - Now, we can change the `sum` procedure so that it generates an iterative process, and all the specific procedures using `sum` will benefit.

## Part 2
#### Higher-order procedures
- We use abstraction to make programs easier to read and write.
- Higher-order procedures increase our abstraction capabilities: they can take other procedures as arguments and return new procedures.
- Our square root algorithm was a specific instance of the more general fixed-point search algorithm. Expressing this directly requires higher-order procedures.
- Damping is a general signal processing strategy. Using a higher-order procedure, we can write programs that use damping as a building block.

## Part 3
#### Newton's method
- Newton's method is a general technique for finding zeros of a function.
- We can implement Newton's method in terms of the fixed-point procedure.
- Top-down design allows us to use names of procedures that we haven't defined yet while writing a program.

#### The rights and privileges of first-class citizens
- To be named by variables
- To be passed as arguments to procedures
- To be returned as values of procedures
- To be incorporating into data structures.
---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- 
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
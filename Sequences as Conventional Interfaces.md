---
share: true
---

up:: [Building Abstractions With Data](./SICP.md#^d1c4f8)
tags::  #map #mapcat #sequences

# Sequences as Conventional Interfaces
- Abstractions preserves the flexibility to experiment with alternative representations
- To use of *conventional interfaces* is another powerful design principle
- To make abstract operations for things other than numbers, we need to have a conventional style in which we manipulate data.

## Sequence operations

^99215e

- We want to organize programs to reflect *signal-flow* structure. To do this, 
	- We focus on the signals and represent them as lists
	- Implement sequence operations on them.
- Expressing programs as sequence operations helps us make program designs that are *modular* - made of relatively independent pieces that we can connect in flexible ways.
	- This is a strategy for controlling complexity.
- A surprisingly vast range of operations can be expressed as sequence operations.
- Sequences serve as a conventional interface for the modules of the program.

> [!INFO]  Data Abstraction
>  - One of the reasons for the success of Lisp as a programming language is that lists provide a standard medium for expressing ordered collections so that they can be manipulated using higher-order operations.
>  - The programming language APL owes much of its power and appeal to a similar choice.
> 	 - In APL, all data are represented as arrays, and there is a universal and convenient set of generic operators for all sorts of array operations

## Nested mappings

^38bc82

- For many computations, the sequence paradigm can be used instead of loops.
- Sometimes we need `nested mappings`, where each mapping maps to a second se of mappings. We can use `mapcat` to flatten the result into one list at the end.
- The procedure for computing all permutations of a set is pure magic:
	- this is wishful thinking in action!

```Scheme 
(define (permutations s)
  (if (null? s)
      (list nil)
      (mapcat (lambda (x)
                (map (lambda (p) (cons x p))
                     (permutations (remove x s))))
              s)))
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
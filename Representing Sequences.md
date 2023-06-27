---
share: true
---

up:: [ Hierarchical Data and the Closure Property](./SICP.md#^25846d)
tags:: #sequences



# Representing Sequences
- One thing we can build with pairs is a *sequence*: an ordered collection of data objects.
- Sequences can be represented by chains of pairs where each `car` points to a value and each `cdr` points to the next pair.
	- The final pair's `cdr` is a special value, `nil`
- For example, `(cons 1 (cons 2 (cons 3 (cons 4 nil))))` represents a sequence:
	![400](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230626164352.png)

- This way of nesting pairs (ending in `nil`) is called *a list*. We usually represent lists by placing each element one after the other and enclosing the whole thing in parentheses.
- Difference between pair and list
```Scheme
> (cons 1 (cons 2 (cons 3 (cons 4 nil))))
(1 2 3 4)
> (cons 1 (cons 2 (cons 3 (cons 4 5))))
(1 2 3 4 . 5) ;; pay attention to the last element!!!, it is a pair!
```
- The procedure `car` gives us the first item; `cdr` gives us the sublist containing all elements but the first; `cons` returns a list with an item added to the front.
- The `nil` value can be thought of as an empty list.

> [!INFO]  List vs List Structure
> - We use *list* to mean a chain of pairs terminated by the end-of-list marker
> - In contrast, the term *list-structure* refers to any data structure made out of pairs, not just to lists.

## List Operations

^49e52f

- We can get the $n^{th}$ item of a list by `cdr` ing `n-1` times and then taking car.

```Scheme
(define (list-ref items n)
  (if (= n 0)
      (car items)
      (list-ref (cdr items)
                (- n 1))))
```

- Scheme includes a primitive predicate `null?` which is true if its argument is `nil`

- We often write recursive procedures that `cdr` all the way through the list
```Scheme
(define (length items)
  (if (null? items)
      0
      (+ 1 (length (cdr items)))))
```

- We can build up lists to return by `cons` in them up:

```Scheme
(define (append fst snd)
  (if (null? fst)
      snd
      (cons (car fst)
            (append (cdr fst)
                    snd))))
```


## Mapping over lists

^da90e1

- The higher-order procedure `map` applies the same transformation to each element in a list, producing a new list

```Scheme
(define (map f xs)
  (if (null? xs)
      nil
      (cons (f (car xs))
            (map f (cdr xs)))))
```

- For example, `(map abs (list -1 5 -3 0 2 -2))` gives the list `(1 5 3 0 2 2)`
- `map` establishes a higher level of abstraction for dealing with lists; it suppresses the recursive detail.
	- We think about the process differently when we use `map`

> [!INFO]  Map Abstraction
> - This abstraction gives us the flexibility to change the low-level details of how sequences are implemented, while preserving the conceptual framework of operations that transform sequences to sequences.
---
## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [List Operations](Representing%20Sequences.md#^49e52f)
	- [ Exercise 17 ](SICPE%202.17.md)
	- [ Exercise 18 ](SICPE%202.18.md)
	- [ Exercise 19 ](SICPE%202.19.md)
	- [ Exercise 20 ](SICPE%202.20.md)
- [ Mapping Over Lists](Representing%20Sequences.md#^da90e1)
	- [ Exercise 21 ](SICPE%202.21.md)
	- [ Exercise 22 ](SICPE%202.22.md)
	- [ Exercise 23 ](SICPE%202.23.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
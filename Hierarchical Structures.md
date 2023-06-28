---
share: true
---

up:: [ Building Abstractions With Data](./SICP.md#^d1c4f8)
tags:: #hierarchical_structures

# Hierarchical Structures
- We can represent lists whose elements themselves are also lists
- We can also think of these structures as trees.
- Recursion is a natural tool for dealing with trees.
- The primitive predicate `pair?` returns true if its argument is a pair.
- We can count the number of leaves in a tree like so:
```Scheme
(define (count-leaves x)
  (cond ((null? x) 0)
        ((not (oair? x)) 1)
        (else (+ (count-leaves (car x))
                 (count-leaves (cdr x))))))
```

## Mapping over trees

^e5bb82

- We can deal with trees using map together with recursion
- This allows us to apply an operation to all the leaves in a tree.

---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [Hierarchical Structures](Hierarchical%20Structures.md)
	- [ Exercise 24 ](SICPE%202.24.md)
	- [ Exercise 25 ](SICPE%202.25.md)
	- [ Exercise 26 ](SICPE%202.26.md)
	- [ Exercise 27 ](SICPE%202.27.md)
	- [ Exercise 28 ](SICPE%202.28.md)
	- [ Exercise 29 ](SICPE%202.29.md)
- [Mapping Over Trees](Hierarchical%20Structures.md#^e5bb82)
	- [ Exercise 30 ](SICPE%202.30.md)
	- [ Exercise 31 ](SICPE%202.31.md)
	- [ Exercise 32 ](SICPE%202.32.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
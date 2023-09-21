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
        ((not (pair? x)) 1)
        (else (+ (count-leaves (car x))
                 (count-leaves (cdr x))))))
```

## List of List representation of trees
- Here is a tree, representation
![400](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230729162614.png)

- Here is how we would do it in Scheme:
```Scheme
`("a" 
	  ("b" 
		  ("d" () ()) 
		  ("e" () ())
	   ) 
	   ("c" 
			("f" () ()) 
			()
		)
)
```

- Here is basic operations example on the binary tree shown above:
```Scheme
(define (root t)
  (car t))

(define (lst t)
  (cadr t))

(define (rst t)
  (cddr t))

(let ((a `("a" ("b" ("d" () ()) ("e" () ())) ("c" ("f" () ()) ()))))
  (display (root a))
  (display "\n")
  (display (lst a) )
  (display "\n")
  (display (rst a) )
  (display "\n")
  (display (lst (lst a))))

> a
(b (d () ()) (e () ()))
((c (f () ()) ()))
(d () ())
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
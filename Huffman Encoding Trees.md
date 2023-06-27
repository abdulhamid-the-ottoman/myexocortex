---
share: true
---

up:: [ Symbolic Data](SICP.md#^369430%20)
tags:: #huffman #encoding #huffman_tree


# Huffman Encoding Trees
- A code is a system for converting information (such as text) into another form.
- ASCII is a fixed-length code: 
	- each symbol uses the same number of bits.
- Morse code is a variable-length code.
	- since `e` is the most common letter, it uses a single dot.
- The problem with variable-length codes is that you must have a way of knowing you have reached the end of a symbol.
	- Morse code uses a temporal pause.
- Prefix codes, such as Huffman encoding, ensures that no code for a symbol is a prefix of the code for another symbol. This eliminates the ambiguity.
- A huffman code can be represented as a binary tree where 
	- each leaf contains a symbol and its weight(relative frequency)
	- each internal node contains the set of symbols and the sum of weights below it.
	- Zero means "go-left", One means "go-right"


## Generating Huffman trees
- Huffman gave an algorithm for constructing the best code for a given set of symbols and their relative frequencies:
	1. Begin with all symbols and their weights as isolated leaves
	2. Form an internal node branching off to the two least frequent symbols
	3. Repeat until all nodes are connected.

## Representing Huffman trees
- Leaves are represented by `(list 'leaf symbol weight)`
- Internal nodes are represented by `(list left right symbols weight)`
	- where `left` and `right` are subtrees. 
	- `symbols` is a list of the symbols underneath the node.
	- `weight` is the sum of the weights of all the leaves beneath the node.

## The decoding procedure
- The following procedure decodes a list of bits using a Huffman tree:
```Scheme
#lang sicp

(define (choose-branch bit branch)
  (cond ((= bit 0) (left-branch branch))
        ((= bit 1) (right-branch branch))
        (else (error "bad bit" bit))))

(define (decode bits tree)
  (define (decode-1 bits current-branch)
    (if (null? bits)
        `()
        (let ((next-branch (choose-branch (car bits) current-branch)))
          (if (leaf? next-branch)
              (cons (symbol-leaf next-branch)
                    (decode-1 (cdr bits) tree))
              (decode-1 (cdr bits) next-branch)))))
  (decode-1 bits tree))
```


## Sets of weighted elements
- Since the tree-generating algorithm requires repeatedly finding the smallest item in a set,
	- we should represent a set of leaves and trees as a list ordered by weight.
- The implementation of `adjoin-set` is similar to [ Exercise 61](SICPE%202.61.md), except that we compare items by weight, and the element being added is not present in the set.

```Scheme
(define (adjoin-set x set)
  (cond ((null? set) (list x))
        (< (weight x) (weight (car set))) (cons x set)
        (else (cons (car set)
                    (adjoin-set x (cdr set))))))
```

---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [ Exercise 67 ](SICPE%202.67.md)
- [ Exercise 68 ](SICPE%202.68.md)
- [ Exercise 69 ](SICPE%202.69.md)
- [ Exercise 70 ](SICPE%202.70.md)
- [ Exercise 71 ](SICPE%202.71.md)
- [ Exercise 72 ](SICPE%202.72.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
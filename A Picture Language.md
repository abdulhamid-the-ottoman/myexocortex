---
share: true
---

up::[ Building Abstractions with Data](./SICP.md#^d1c4f8) 
tags:: #picture_language

# A Picture Language

- In this section, we will create a simple language for drawing pictures
- The data objects are represented as procedures, not as list structure.

## The picture language

^32d750

- There is only one kind of element, called *painter*
- The painter draws an image transformed into parallelogram
- We combine images with operations like `beside` and `below`
- We transform single images with operations like `flip-vert` and `flip-horiz`
- We can build up complexity easily thanks to closure : the pointers are closed under the language's means of combination. For example:

```Scheme
(define (flipped-pairs painter) 
  (let ((painter2 (beside painter (flip-vert painter)))) 
	  (below painter2 painter2)))
```

## Higher -order operations

^e3c6e4

- Just as we have higher-order procedures, we can have higher-order painter operations.
- We can manipulate the painter operations rather than manipulating the painters directly.
- Here is an example higher-order painter operation:

```Scheme
(define (square-of-four tl tr bl br) 
  (lambda (painter)
   (let ((top (beside (tl painter) (tr painter))) 
			(bottom (beside (bl painter) (br painter)))) 
   (below bottom top))))
```


## Frames

^a2a8cb

- Painters paint their contents in `frames`
- A frame parallelogram can be represented by an origin vector and two edge vectors.
- We will use coordinates in the unit square to specify images
- We can use basic vector operations to map an image coordinate into pair of coordinates within the frame.

## Painters

^0b9c64

- A painter is a procedure that takes a frame as an argument and draws its image transformed to fit in the frame.
- The details of primitive painters depend on the characteristics of the graphics system.
- Representing painters as procedures creates a powerful abstraction painter.


## Transforming and combining painters

^a99c26

- Operations on painters invoke the original painters with new frames derived from the argument frame.
- They are all based on procedure `transform-painter`


## Levels of language for robust design

^e8eb23

- The fundamental data abstractions in the picture language are painters.
	- Representing them as procedures makes all the tools of procedural abstraction available to us.
- This example also uses **stratified design**, the notion that a complex system should be structured as sequence of levels.
- Each time we start a new level, we treat the old complex things as primitive black boxes and combine them.

> [!INFO]  Stratified Design
>  - Stratified design helps make programs robust, that is, it makes it likely that small changes in a specification will require correspondingly small changes in the program.
>  - In general, each level of a stratified design provides a different vocabulary for expressing the characteristics of the system, and a different kind of ability to change it.


---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [ The Picture Language](A%20Picture%20Language.md#^32d750%20)
	- [ Exercise 44](SICPE%202.44.md)
- [ Higher-order Operations](A%20Picture%20Language.md#^e3c6e4)
	- [ Exercise 45](SICPE%202.45.md)
- [ Frames](A%20Picture%20Language.md#^a2a8cb)
	- [ Exercise 46](SICPE%202.46.md)
	- [ Exercise 47](SICPE%202.47.md)
- [Painters](A%20Picture%20Language.md#^0b9c64)
	-  [Exercise 48](SICPE%202.48.md)
	- [ Exercise 49](SICPE%202.49.md)
- [ Transforming and combining painters](A%20Picture%20Language.md#^a99c26)
	- [ Exercise 50](SICP%202.50.md)
	-  [Exercise 51](SICPE%202.51.md)
- [ Levels of language for robust design](A%20Picture%20Language.md#^e8eb23)
	- [ Exercise 52](SICPE%202.52.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
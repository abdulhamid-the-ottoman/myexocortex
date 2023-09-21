---
share: true
---

up:: [Systems with Generic Operations](./SICP.md#^daebf9)
tags:: 

# Symbolic Algebra

- Manipulating symbolic algebraic expressions is hard.
- We can view them as trees of operators applied to operands
- To keep things simple, we'll stick to polynomials

## Arithmetic on polynomials
- Polynomials are expressed in terms of variables called `indeterminates`
- A `univariate` (single indeterminate) has the form $c_0$ + $c_1x$ + $c_2x^2$ + ... + $c_nx^n$
- To avoid thorny issues of identity and sameness, we will consider our polynomials to be syntactic forms, not representations of mathematical functions.
- We will implement addition and multiplication for polynomials in the same variable.

```Scheme
(define (add-poly p1 p2)
  ;; same indeterminate check
  (if (same-variable? (variable p1) (variable p2)) 
      (make-poly (variable p1) ;; variable
			      ;; add the terms of polynomials
                 (add-terms (term-list p1) 
                            (term-list p2)))
        ;; different indeterminate, we can't add!
      (error "polys not in same var" p1 p2)))

(define (mul-poly p1 p2)
  ;; same indeterminate check
  (if (same-variable? (variable p1) (variable p2)) 
      (make-poly (variable p1)
			      ;; multiply all terms
                 (mul-terms (term-list p1) 
                            (term-list p2)))
      (error "polys not in same var" p1 p2)))
```

- We will install these procedures in our generic arithmetic system:

```Scheme
(define (install-polynomial-package)
  ;; Internal procedures
  (define (make-poly variable term-list)
    (cons variable term-list))
  (define (variable p) (car p))
  (define (term-list p) (cdr p))
  (define (add-poly p1 p2) ...)
  (define (mul-poly p1 p2) ...)

  ;; Interface to rest of the system
  (define (tag p) (attach-tag 'polynomial p))
  (put 'add '(polynomial polynomial)
       (lambda (p1 p2) (tag (add-poly p1 p2))))
  (put 'mul '(polynomial polynomial)
       (lambda (p1 p2) (tag (mul-poly p1 p2))))
  (put 'make 'polynomial
       (lambda (var terms) (tag (make-poly var terms))))
  'done)
```

- Here is the implementation of `add-terms` :
```Scheme

(define (add-terms L1 L2)
  (cond ((empty-termlist? L1) L2)
        ((empty-termlist? L2) L1)
        (else
         (let ((t1 (first-term L1)) (t2 (first-term L2)))
           ;;t1 has a higher order than t2
           (cond ((> (order t1) (order t2))
                  (adjoin-term
                   t1 (add-terms (rest-terms L1) L2)))
                 ;;t2 has a higher order than t1
                 ((< (order t1) (order t2))
                  (adjoin-term
                   t2 (add-terms L1 (rest-terms L2))))
                 (else
                  ;;both has the same order to be summed
                  (adjoin-term
                   (make-term (order t1)
                              (add (coeff t1) (coeff t2)))
                   (add-terms (rest-terms L1)
                              (rest-terms L2)))))))))
```

- Since it uses the generic add internally, the system automatically works with polynomials whose coefficients are themselves polynomials in a different variable!

## Representing term lists

^d3f120

- Our procedures `add-terms` and `mul-terms` always access terms sequentially from highest to lowest order, so we need some kind of ordered representation.
- For *dense* polynomials (mostly nonzero coefficients), a simple list is best.
	- Ex: $x^5$ + $2x^4$ + $3x^2$ - $2x$ -5 becomes `'(1 2 3 -2 -5)`
	- we know the highest order (5) , we can go over term list by decreasing
- For *sparse* polynomials (mostly zero coefficients), an associative list is best
	- Ex: $x^{100}$ + $2x^2$ + 1 becomes `'((100,1) (2,2) (0 1))`
- Here is an associative list representation:
```Scheme
(define (adjoin-term term term-list)
  (if (=zero? (coeff term))
      term-list
      (cons term term-list)))
(define (the-empty-termlist) '())
(define (first-term term-list) (car term-list))
(define (rest-terms term-list) (cdr term-list))
(define (empty-termlist? term-list) (null? term-list))
(define (make-term order coeff) (list order coeff))
(define (order term) (car term))
(define (coeff term) (cadr term))
```

- Users of the polynomial package will create (tagged) polynomials by means of the procedure:

```Scheme
(define (make-polynomial var terms)
  (get 'make 'polynomial) var terms)
```

## Hierarchies of types in symbolic algebra

^903d5c

-  The data types in our polynomial algebra can't easily be arranged in a tower.
- For example, how would we coerce (x+1)$y^2$  and (y+1)$x^2$ to a common type?
	- (y+1)$x^2$ is a polynomial in x whose coefficients are polynomials in y
	- (x+1)$y^2$ is a polynomial in y whose coefficients are polynomials in x
-  Neither of these types is "above" the other in any natural way,  yet it is often necessary to add together elements from each set.
	- One possibility is to convert one polynomial to the type of the other by expanding and rearranging terms so that both polynomials have the same principal variable.
- One can impose a tower-like structure on this by ordering the variables and thus always converting any polynomial to *canonical form* with the highest-priority variable dominant and the lower-priority variables buried in the coefficients
	- This strategy works fairly well, except that the conversion may expand a polynomial unnecessarily, making it hard to read and perhaps less efficient to work with.
- The tower strategy is certainly not natural for this domain or for any domain where the user can invent new types dynamically using old types in various combining forms, such as trigonometric functions, power series and integrals.

> [!INFO]  Coercion Problem
>  - It should not be surprising that controlling coercion is a serious problem in the design of large-scale algebraic manipulation systems.
>  - Much of the complexity of such systems is concerned with relationships among diverse types.
>  - Indeed, it is fair to say that we don't yet completely understand coercion.
>  - In fact, we do not yet completely understand the concept of data type.
>  - Nevertheless, what we know provides us with powerful structuring and modularity principles to support the design of large systems.


## Extended exercise: Rational functions

^5d6767

- *Rational functions are fractions* with polynomial numerators and denominators.
	- Ex : $\frac{(x+1)}{x^3 - 1}$
- we need to be able to add, subtract, multiply and divide rational functions and to perform computations such as 
	![400](./40-referenceVAULTS/Resource%20Library/Images/Image-1.jpg)

- We can use our rational package from [Generic Arithmetic Operations](./Generic%20Arithmetic%20Operations.md) , but we need to change a few things.
- To reduce rational functions, we need to be able to compute the GCD of polynomials, which in turn requires computing the remainder after polynomial division.
- To avoid fractional coefficients, we can multiply the result by an *integerizing factor*
- Here is our algorithm for reducing a rational function to lowest terms:
	1. Compute the integerized GCD of numerator and denominator.
	2. Multiply the numerator and denominator by an integerizing factor:
		- the leafing coefficient of the GCD raised to the power 1 + max{ $O_N$ , $O_D$ } - $O_G$, where 
			- $O_N$ is the order of the numerator
			- $O_D$ is the order of the denominator
			- $O_G$ is the order of the GCD
	3. Divide the result of (2) by the GCD from (1)
	4. Divide the results of (3) by the GCD of all their coefficients
 - The GCD algorithm is at the heart of every system that does operations on rational functions.
	 - Ours is very slow.
	 - Probabilistic algorithms like Zippel's are faster.
 
## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [ Representing Term Lists](Symbolic%20Algebra.md#^d3f120)
	- [ Exercise 87 ](SICPE%202.87.md)
	- [ Exercise 88 ](SICPE%202.88.md)
	- [ Exercise 89 ](SICPE%202.89.md)
	- [ Exercise 90 ](SICPE%202.90.md)
	- [ Exercise 91 ](SICPE%202.91.md)
- [ Hierarchies of types in symbolic algebra](Symbolic%20Algebra.md#^903d5c)
	- [ Exercise 92](SICPE%202.92.md)
- [ Rational Functions](Symbolic%20Algebra.md#^5d6767)
	- [ Exercise 93 ](SICPE%202.93.md)
	- [ Exercise 94 ](SICPE%202.94.md)
	- [ Exercise 95 ](SICPE%202.95.md)
	- [ Exercise 96 ](SICPE%202.96.md)
	- [ Exercise 97 ](SICPE%202.97.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
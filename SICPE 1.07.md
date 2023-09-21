---
created: ["2023-06-12 10:52"]
share: true
---

up::[SICP-Chapter1-Exercises](./SICP-Chapter1-Exercises.md)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> The `good-enough?` test used in computing square roots will not be very effective for finding the square roots of very small numbers. 
> Also, in real computers, arithmetic operations are almost always performed with limited precision. 
> This makes our test inadequate for very large numbers. Explain these statements, with examples showing how the test fails for small and large numbers. 
> An alternative strategy for implementing good-enough? is to watch how guess changes from one iteration to the next and to stop when the change is a very small fraction of the guess. Design a square-root procedure that uses this kind of end test. Does this work better for small and large numbers?


## 🔑 **Key Points of Understanding**
- This is a very interesting exercise because it forces to look at “behind the scenes” at how computer handle certain kinds of numbers. 
- It also shows that you need to have this kind of knowledge in order to develop correct programs.
- Here is a few examples showing us what happens with the interpreter:
```scheme
(sqrt 1234567890123)
> 1111111.1061109055

(sqrt 12345678901234)
does not finish

(sqrt 12345678901230)
> 3513641.828819494

(sqrt 0.00000000123)
> 0.031250013107186406

(square (sqrt 0.00000000123))
> 0.000976563319199322
```
- From this we can see two problems:
	- With large numbers, most of the time the computation doesn't finish. Example: `(sqrt 12345678901234)`
	- With small numbers, the result can be very inaccurate, by multiple orders of magnitude. Example : `(square (sqrt 0.00000000123))` will end up with ` 0.000976563319199322`. This results $10^4$ difference.
	
- In order to understand what is happening, we need to look at how real numbers are encoded in computers, more specifically "floating point" encoding.

- Key facts about floating point numbers:
	- Because each number is encoded on a finite number of bits, the number of floating point numbers that can be represented in a computer is finite.
	- Most of the time, a floating point number is an approximation of a real number. This causes rounding issues.
	- As the size of the number represented increases, the size of the 'gap' between 2 consecutive numbers will increase step by step.
	
- Squeezing infinitely many real numbers into a finite number of bits requires an approximate representation. Although there are infinitely many integers, in most programs the result of integer computations can be stored in 32 bits. 
	- In contrast, given any fixed number of bits, most calculations with real numbers will produce quantities that cannot be exactly represented using that many bits. Therefore the result of a floating-point calculation must often be rounded in order to fit back into its finite representation. This rounding error is the characteristic feature of floating-point computation.
# 🔍 Solutions
- The first step is to redefine `good-enough?` based on the definition from the problem statement:
```scheme
(define (good-enough? previous-guess guess)
  (< (abs (/ (- guess previous-guess) guess)) 0.00000000001))
```

- The number is somewhat arbitrary `0.00000000001` is based on a few trial and error for the upcoming tests. Then we just need to adapt the function `sqrt-iter` to provide the correct argument:

```scheme
(define (sqrt-iter guess x)
  (if (good-enough? guess (improve guess x))
      guess
      (sqrt-iter (improve guess x) x)))
```

- Although we could improve the code to avoid computing `(improve guess x)` twice, the method to do this is not learned yet learned at this time in the book.

- The complete solution is:
```scheme
(define (square x) (* x x))

(define (good-enough? previous-guess guess)
  (< (abs (/ (- guess previous-guess) guess)) 0.00000000001))

(define (sqrt-iter guess x)
  (if (good-enough? guess (improve guess x))
      guess
      (sqrt-iter (improve guess x) x)))

(define (improve guess x)
  (average guess (/ x guess)))

(define (average x y)
  (/ (+ x y) 2))

(define (sqrt x)
  (sqrt-iter 1.0 x))
```

- it is interesting to note that the new `good-enough?` doesn't depend `x` anymore.
- We can try larger numbers:
```Scheme
(sqrt 123456789012345) = 11111111.061111081 - Error: 0.015625
```

- and small numbers:
```Scheme
(sqrt 0.00000000123456) = 3.51363060095964e-05 - Error: 4.1359030627651384e-25
```

- In both cases, the error is small relative to the size of the number computed.!!!

# 🧠 Ideas about Problem
#### Large Numbers
- For most numbers above a certain size of digits, the computation of the square root will never finish.
- When tracing the program step by step, we can see that this condition happens for large numbers when the guess is getting very close to the actual result. Because of rounding errors, the function `(improve guess x)` can’t improve the guess anymore as the smallest possible difference between guess2 and x is larger than `0.001`.
- This is because with a number of this order of magnitude, the distance between two consecutive floating point numbers is larger than `0.001`.

- For example, here is the trace for `(sqrt 12345678901234)` :

| iteration | guess             | (imrove guess x)   | (- (square guess) x)   |
| --------- | ----------------- | ------------------ | ---------------------- |
| 0         | 1.0               | 6172839450617.5    | -12345678901233.0      |
| 1         | 6172839450617.5   | 3086419725309.75   | 3.8103946883087414e+25 |
| 2         | 3086419725309.75  | 1543209862656.875  | 9.525986720768766e+24  |
| 3         | 1543209862656.875 | 771604931332.4375  | 2.3814966801891054e+24 |
| 4         | 771604931332.4375 | 385802465674.21875 | 5.953741700441899e+23  |
|5|385802465674.21875|192901232853.10938|1.4884354250796105e+23|
|6|192901232853.10938|96450616458.55469|3.7210885623903846e+22|
|7|96450616458.55469|48225308293.27734|9.302721402889541e+21|
|8|48225308293.27734|24112654274.63867|2.3256803476359655e+21|
|9|24112654274.63867|12056327393.319334|5.8142008382257175e+20|
|10|12056327393.319334|6028164208.659653|1.4535501786922326e+20|
|11|6028164208.659653|3014083128.3297105|3.6338751380886356e+19|
|12|3014083128.3297105|1507043612.1639276|9.084684758802912e+18|
|13|1507043612.1639276|753525902.074542|2.2711681032851973e+18|
|14|753525902.074542|376771142.9778979|5.677889394183511e+17|
|15|376771142.9778979|188401955.01397642|1.4194414850197034e+17|
|16|188401955.01397642|94233741.7076047|3.548295097418716e+16|
|17|94233741.7076047|47182376.47141617|8867652397314325.0|
|18|47182376.47141617|23722017.581583798|2213830970589212.0|
|19|23722017.581583798|12121224.408177208|550388439239736.8|
|20|12121224.408177208|6569870.942541849|134578402252156.9|
|21|6569870.942541849|4224503.311279173|30817525300421.72|
|22|4224503.311279173|3573450.5222935397|5500749325774.699|
|23|3573450.5222935397|3514142.3366335463|423869734045.97266|
|24|3514142.3366335463|3513641.86446291|3517460886.28125|
|25|3513641.86446291|3513641.8288200637|250472.396484375|
|26|3513641.8288200637|3513641.8288200637|0.001953125|
|27|3513641.8288200637|3513641.8288200637|0.001953125|
|28|3513641.8288200637|3513641.8288200637|0.001953125|          |                   |                    |                        |

- if we are lucky, the rounding errors give that `(- (square guess) x)` is evaluated exactly to 0.0 and the evaluation stops.

- if we are unlucky, the gap between 2 consecutive numbers around `(square guess)` is more than `0.001` and the assertion `good-enough?` will never become true. `improve` has reached a fixed point due to the rounding error, and will always return the same number that is larger than `0.001`. 
	- Here is an example:
 ```scheme
(improve 3513641.8288200637 12345678901234) -> 3513641.8288200637
```

#### Small Numbers
- The problem is this case is different. We have hardcoded the number of digits of precision we want. It means that we can’t have an accurate answer if x is smaller than the precision of `0.001`.

```scheme
(sqrt 0.00000000123456) = 0.0312500131557789 - Error: 0.0009765620876763541
```

- Looking at the trace, we see that it stops iterating quickly, because the test to check the accuracy of the result think that this is good enough:

| iteration | guess               | (improve guess x)    | (- (square guess) x)  |     |     |     |     |
| --------- | ------------------- | -------------------- | --------------------- | --- | --- | --- | --- |
| 0         | 1.0                 | 0.50000000061728     | 0.99999999876544      |     |     |     |     |
| 1         | 0.50000000061728    | 0.2500000015432      | 0.24999999938272      |     |     |     |     |
| 2         | 0.2500000015432     | 0.12500000324072     | 0.06249999953704      |     |     |     |     |
| 3         | 0.12500000324072    | 0.06250000655859987  | 0.01562499957562001   |     |     |     |     |
| 4         | 0.06250000655859987 | 0.0312500131557789   | 0.0039062495852650275 |     |     |     |     |
| 5         | 0.0312500131557789  | 0.015625026330841132 | 0.0009765620876763541 |     |     |     |     |
|           |                     |                      |                       |     |     |     |     |


# 🔗 Related Applications


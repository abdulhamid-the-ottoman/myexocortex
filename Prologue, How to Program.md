---
share: true
---

up:: 
tags:: 



# Prologue: How to Program

![Pasted image 20230802133252.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802133252.png)
- The top half of DrRacket is called the *definitions area.** In this area, you create the programs, which is called editing.
- - Programs consist of expressions. You have seen expressions in mathematics. For now, an expression is either a plain number or something that starts with a left parenthesis “(” and ends in a matching right parenthesis “)”—which DrRacket rewards by shading the area between the pair of parentheses.
- When you click RUN, DrRacket evaluates the expressions in the definitions area and shows their result in the *interactions area.* Then, DrRacket, your faithful servant, awaits your commands at the prompt (>).
	- The appearance of the prompt signals that DrRacket is waiting for you to enter additional expressions, which it then evaluates like those in the definitions area:
![100](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802133544.png)
- Take a close look at the last number. Its **“#i” prefix** is short for “I don’t really know the precise number so take that for now” or an inexact number.
	-  When it doesn’t know the exact number, it warns you with this special prefix

- By now you might be wondering whether DrRacket can add more than two numbers at once, and yes, it can! As a matter of fact, it can do it in two different ways:
![200](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802133754.png)
	- The first one is nested arithmetic, as you know it from school
	- The second one is BSL arithmetic; and the latter is natural, because in this notation you always use parentheses to group operations and numbers together.
- Every time you want to use a “calculator operation,” you write down an opening parenthesis, the operation you wish to perform, say +, the numbers on which the operation should work (separated by spaces or even line breaks), and, finally, a closing parenthesis
	- The items following the *operation* are called the *operands.*

## Arithmetic and Arithmetic
- If programming were just about numbers and arithmetic, it would be as boring as mathematics. Fortunately, there is much more to programming than numbers: text, truths, images, and a great deal more.
		![300](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802134546.png)

 - Just like [+](http://docs.racket-lang.org/htdp-langs/beginner.html#%28def._htdp-beginner._%28%28lib._lang%2Fhtdp-beginner..rkt%29._%2B%29%29),  [string-append](http://docs.racket-lang.org/htdp-langs/beginner.html#%28def._htdp-beginner._%28%28lib._lang%2Fhtdp-beginner..rkt%29._string-append%29%29) is an operation; it makes a string by adding the second to the end of the first.
		 ![Pasted image 20230802134803.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802134803.png)
- [string-append](http://docs.racket-lang.org/htdp-langs/beginner.html#%28def._htdp-beginner._%28%28lib._lang%2Fhtdp-beginner..rkt%29._string-append%29%29), like [+](http://docs.racket-lang.org/htdp-langs/beginner.html#%28def._htdp-beginner._%28%28lib._lang%2Fhtdp-beginner..rkt%29._%2B%29%29), can handle as many operands as desired.
- You can do more with strings than append them. You can 
	- extract pieces from a string, 
	- reverse them, 
	- render all letters uppercase (or lowercase), 
	- strip blank spaces from the left and right, and so on.
- If you looked up the primitive operations of BSL, you saw that *primitive (sometimes called pre-defined or built-in) operations can consume strings and produce numbers:
	![Pasted image 20230802140310.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802140310.png)
- There is also an operation that converts strings into numbers:
	![Pasted image 20230802140409.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802140409.png)
	- What happens if i feed this operation string->number a non-number literal, here is what happens:
		![Pasted image 20230802140529.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802140529.png)
- Boolean values come in only two varieties: `#true` and `#false`
	![200](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802140651.png)
- It is also useful to see comparison of 2 numbers result in a boolean
	![200](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802140745.png)

- Here is an elaborate nested arithmetic example:
```Scheme
(and (or (= (string-length "hello world")
            (string->number "11"))
         (string=? "hello world" "good morning"))
     (>= (+ (string-length "hello world") 60) 80))

#false
```

### Images
- Before we show you how to do some “real” programming, let’s discuss one more kind of data to spice things up: images
	- In order to this, we will add **(require 2htdp/image)** to the definitions area, or select Add Teachpack from the Language menu and choose image from the Preinstalled HtDP/2e Teachpack menu.
	- Using  libraries is just like expanding your vocabularies with new words or your programming vocabulary with new primitives
- Here is an example:
```Scheme
;; this is like adding a library to be used in our program
;;Makes the definitions of the module specified by string available in the current module (i.e., the current file)
(require 2htdp/image)

(circle 10 "solid" "red")
(rectangle 30 20 "outline" "blue")
```
![Pasted image 20230802141952.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802141952.png)

- a BSL program deals with images as data that is just like numbers. In particular, BSL has operations for combining images in the same way that it has operations for adding numbers or appending strings:
	![Pasted image 20230802142157.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802142157.png)

- Overlaying these images in the opposite order produces a solid blue square:
	![Pasted image 20230802143103.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802143103.png)

- As you can see, [overlay](http://docs.racket-lang.org/teachpack/2htdpimage.html#%28def._%28%28lib._2htdp%2Fimage..rkt%29._overlay%29%29) is more like [string-append](http://docs.racket-lang.org/htdp-langs/beginner.html#%28def._htdp-beginner._%28%28lib._lang%2Fhtdp-beginner..rkt%29._string-append%29%29) than [+](http://docs.racket-lang.org/htdp-langs/beginner.html#%28def._htdp-beginner._%28%28lib._lang%2Fhtdp-beginner..rkt%29._%2B%29%29), but it does “add” images just like [string-append](http://docs.racket-lang.org/htdp-langs/beginner.html#%28def._htdp-beginner._%28%28lib._lang%2Fhtdp-beginner..rkt%29._string-append%29%29) “adds” strings and [+](http://docs.racket-lang.org/htdp-langs/beginner.html#%28def._htdp-beginner._%28%28lib._lang%2Fhtdp-beginner..rkt%29._%2B%29%29) adds numbers.

![Pasted image 20230802143243.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802143243.png)

- Here is another illustration of the same idea:
	![Pasted image 20230802144311.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802144311.png)

- Two more operations matter: [empty-scene](http://docs.racket-lang.org/teachpack/2htdpimage.html#%28def._%28%28lib._2htdp%2Fimage..rkt%29._empty-scene%29%29) and [place-image](http://docs.racket-lang.org/teachpack/2htdpimage.html#%28def._%28%28lib._2htdp%2Fimage..rkt%29._place-image%29%29). The first creates a scene, a special kind of rectangle. The second places an image into such a scene:
	![Pasted image 20230802144405.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802144405.png)
	- Here is the result
		![100](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802144531.png)
		- As you can see from this  image, the origin (or (0,0)) is in the upper-left corner.
		- Unlike in mathematics, the y-coordinate is measured downward, not upward

### Summary
- To program is to *write down an arithmetic expression*, but you’re no longer restricted to boring numbers.
	- *Arithmetic* is the branch of mathematics dealing with properties and manipulation of numbers. But we can treat booleans, strings and images as numbers.
	- This arithmetic expressions can be in numbers, booleans, strings or images.
	- In BSL, arithmetic is the arithmetic of numbers, strings, Booleans, and even images.
- To compute, though, still means *to determine the value of an expression*—except that this value can be a string, a number, a Boolean, or an image.


## Inputs and Output
- It is good because programming and computing ought to be a natural generalization of using a calculator.
- It is bad because the purpose of programming is to deal with lots of data and to get lots of different results, with more or less the same calculations.

- Your teachers would ask you to fill in the blank, that is, replace the "?" mark with a number.
	 ![Pasted image 20230802145405.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802145405.png)

- It turns out making a move is no more complicated than completing a table of numbers like that.
	![Pasted image 20230802145618.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802145618.png)
-  your teacher should ask you here to draw the fourth image, the fifth, and the 1273rd one because a movie is just a lot of images
- You may also recall that your teacher not only asked for the fourth or fifth number in some sequence but also for an expression that determines any element of the sequence from a given x.
 - We need to define  a function that computes the nth sequence.

### Functions
- Here is how the function definition is done:
	![Pasted image 20230802190731.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802190731.png)
	- It essentially consists of three pieces: two names and an expression
	- The first name is the name of the function; you need it to apply the function as often as you wish.
	- The second name—called a parameter—represents the input of the function, which is unknown until you apply the function.
	- The expression, dubbed body, computes the output of the function for a specific input.
	
- Here is how you apply a function.
	![300](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230802190857.png)
	- The first part tells DrRacket which function you wish to use. 
	- The second part is the input to which you want to apply the function
	
- Here 



## Many Ways to Compute
## One Program, Many Definitions
## One More Definition
## You Are a Programmer Now
## Not!

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
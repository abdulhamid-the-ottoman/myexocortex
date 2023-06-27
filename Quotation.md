---
share: true
---

up:: [ Symbolic Data](./SICP.md#^369430)
tags:: #quotation



# Quotation
- Lists with symbols look just like Lisp code, except we `quote` them.
- To quote in Lisp, we use the special form `(quote exp)`, or the shorthand `'exp`
- For example, `'x` evaluates to the symbol "x" instead of the variable `x`'s value.
- This is like just natural language.
	- If I say, "Say your name" , you will say "Vehbi", 
	- If I instead say, "Say 'your name' ", you will literally say the words "your name"

```Scheme
(define a 1) 
(define b 2) 
(list a b)   ;; → (1 2) 
(list 'a 'b) ;; → (a b) 
(list 'a b)  ;; → (a 2)
```

- Now that we have quotation, we will use `'()` for empty list instead of `nil`
- We need another primitive now: `eq?`. This checks if two symbols are the same.

```Scheme
(eq? 'a 'b) ;; → #f
(eq? 'a 'a) ;; → #t
```
---

## 🔑 Key Points
- 
## ❓ Questions
- 
## 📦 Resources
- [ Exercise 53](SICPE%202.53.md)
- [ Exercise 54](SICPE%202.54.md)
- [ Exercise 55](SICPE%202.55.md)
## 🎯 Actions
- [ ] 
- [ ] 
- [ ] 
- [ ] 
- [ ] 
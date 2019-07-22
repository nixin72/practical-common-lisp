# Functions

- Functions are the core building block of Lisp code
- More than 3/4 of the names in the CL standard are functions
- Since macros run at compile time, they can't actually do as much as functions can.

## Defining functions
---
```scheme
(defun function-name (parameter*)
  "Optional documentation string"
  body-form*)
```
- By convention, names are always hyphenated: No snake_case or camelCase
- The optional documentation string is important because it allows us to extract it using the `documentation` function
- In chapter 2 we defined the "hello-world" function:
  ```scheme
  (defun hello-world () (format t "hello world!"))
  ```
  This function is named "hello-world", takes no arguments, and has a single call in it's body

### Function parameters
- Many different types of parameters:
  - Required
  - Optional
  - List
  - Mapped

#### Optional parameters
```scheme
(defun foo (a b &optional c d) (list a b c d))

(foo 1 2)     ; (1 2 NIL NIL)
(foo 1 2 3)   ; (1 2 3 NIL)
(foo 1 2 3 4) ; (1 2 3 4)
```
Like any other function, there is still a set number of parameters required for this function, it's just now a range.

You can also define default values for the optional parameters instead of `NIL`:
```scheme
(defun foo (a &optional (b 10)) (list a b))

(foo 1)   ; (1 10)
(foo 1 2) ; (1 2)
```
You can also define the default value of a parameter to be the same as that of another parameter:
```scheme
(defun area-rectangle (width &optional (height width)) (* width height))
```
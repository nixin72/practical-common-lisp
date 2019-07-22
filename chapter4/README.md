# Syntax and Semantics

The Lisp language processor (either compiler or interpreter) is broken up into two different pieces. The **reader** and the **evaluator**

## The Reader
---
- The reader deals purely with s-expressions, and doesn't care whether things are valid lisp forms.
- Translates s-expressions into valid lisp forms
- S-expressions are composed of **lists** and **atoms**
  - Lists are parenthesis delimited contain any number of elements separated by whitespace
  - Atoms are everything else
    - numbers
    - strings
    - symbols
    - Empty list

### Numbers
```scheme
123    ; Integer 123
3/7    ; Fraction 3 over 7
1.0    ; Floating point number 1.0
+10    ; Positive integer 10
-10    ; Negative integer 10
-1/4   ; Negative 1 quarter
1.0e0  ; Scientific notation 1 * 10^0
1.0e3  ; Scientific notation 1 * 10^3
1.0d0  ; Scientific notation but using double precision floating points
1.0e-4 ; Scientific notation for 1.0 * 10^-4
```

### Strings
```scheme
"Foo"   ; Foo
"Fo\o"  ; Foo
"Fo\\o" ; Fo\o
"Fo\"o" ; Fo"o
```

### Symbols
- Can contain almost any character *except* whitespace
- Numbers can be in names as long as the whole name can't be interpreted as a number
- A symbol's name can't consist of only periods
- Some characters can only exist in names if they're escaped:
  - `(`, `)`, `'`, `"`, ```, `,`, `:`, `;`, `\` and `|`
- The language standard only uses some characters in symbol names:
  - `[a-zA-Z]`, `*`, `+`, `-`, `/`, `1`, `2`, `<`, `>`, `=` and `&`

## The Evaluator
---
- Evaluates s-expressions as lisp forms
- Not all valid s-expressions are valid lisp forms:
  - Any atom or empty list is legal
  - Any list beginning with a symbol is legal
- The evaluator is essentially a back-end to the compiler.
- Special symbols can be self-evaluating, such as `T` and `NIL`
- Keyword symbols begin with `:`
  - self-evaluating symbol who's name and value are the same

### Function calls
```lisp
(function-name arguments*)
```

### Special operators
- Not all operations can be defined as functions:
  ```lisp
  (if x (format t "yes") (format t "no"))
  ```
  Would print both "yes" and "no" because they're evaluated before being input to the function.
- There are 25 different special operators built into CL, but not all are regularly used.

## Macros
---
- Special operators are fixed by the language standard and are built into the compiler
- Macros can be user defined and aren't a part of the standard
- A macro takes s-expressions as arguments and transforms them into lisp forms that are evaluated
- Macro expansion takes place at *compile time*

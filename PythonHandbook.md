# <img src=https://cdn.freebiesupply.com/logos/large/2x/python-5-logo-svg-vector.svg width=30px> Python Handbook

## Table of Contents
> [Language Details](#language-details) <br>
>> [Commenting](#commenting) <br>

> [Variables](#variables) <br>
>> [Local vs Global Variables](#local-vs-global-variables) <br>

> [Control Flow](#control-flow) <br>
>> [`__name__`](#__name__) <br>
>> [`if-elif-else` Statements](#if-elif-else-statements) <br>
>> [`match-case` Structure](#match-case-structure) <br>
>>> [`match-case` with Lists](#match-case-with-lists) <br>
>>
>> [Loops](#loops) <br>
>>> [`for` Loops](#for-loops) <br>
>>> [`while` Loops](#while-loops) <br>
>>
>> [`try-except`](#try-except) <br>
>> [`pass`](#pass) <br>

> [Built-In Data Types](#built-in-data-types) <br>
>> 
>> [`==` vs `is`](#vs-is) <br>









<br>
<br>
<br>
<br>
<br>
<hr>

## Language Details
- Files end with `.py`.
- All values are objects (instances of a class).

### Commenting
```Python
# single-line comment

"""
multi
line
comment
"""
```









## Variables
- A **variable** is an identifier that refers to an object in memory.
- Variables are **dynamically typed** => a variable takes on the type of the object it refers to at runtime.
```Python
# Assign a value (object) to a variable?
VARIABLE = VALUE

# Chained Assignment
VAR1 = VAR2 = ... = VALUE

# Parallel Assignment
VAR1, VAR2, ... = VAL1, VAL2, ...

# Swap two variables?
VAR1, VAR2 = VAR2, VAR1
```

### Local vs Global Variables
- A **local variable** is a variable that is defined (and accessible) within a function.
- A **global variable** is a variable that is defined (and accessible) within the main body.
- For functions:
  - Parameters are local variables.
  - Global variables must be explicitly declared `global` before assignment. 
```Python
# Declare a variable to be global?
global VARIABLE
```









## Control Flow
### `__name__`
- `__name__` is a variable that exists in every Python file. 
- If a file is run directly, then `__name__ == "__main__"`.
- If a file is imported, then `__name__` is the modules name. 
```Python
# Define a script's entry point?
if __name__ == "__main__":
  MAIN_BODY_CODE
```

### `if-elif-else` Statements
```Python
# General Syntax
if IF_CONDITION:
  IF_CODE
elif ELIF_CONDITION1:
  ELIF_CODE1
elif ELIF_CONDITION2:
  ELIF_CODE2
...
else:
  ELSE_CODE

# Ternary Operator
IF_CODE if CONDITION else ELSE_CODE

# Shorthand If
if CONDITION: CODE
```

### `match-case` Structure
- An **expression** is a piece of code that evaluates to a value (object).
```Python
# General Syntax
match EXPRESSION:
  case VALUE1:
    CASE_CODE1
  case VALUE2:
    CASE_CODE2
  ...
  # Give a case multiple possible values?
  case VALUE1 | VALUE2 | ...:
    CASE_CODE
  # Give a case an extra condition to check?
  case VALUE if CONDITION:
    CASE_CODE
  # Define a default case?
  case _:
    DEFAULT_CODE
```

#### `match-case` with Lists
- Position and length matter.
```Python
match MATCH_LIST:
  # Match each element of the match list exactly?
  case [ELEMENT1, ELEMENT2, ...]:             # construct the case list exactly
    CASE_CODE
  # Use wildcard elements in the case list?
  case [_, _, ...]:
    CASE_CODE
  # Match an arbitrary number of elements of the match list?
  case [..., *VARIABLE, ...]:                 # *VARIABLE takes on zero or more elements such that
    CASE_CODE                                 # case list elements left = match list elements left
```

### Loops
- `for` and `while` loops can have an optional `else` statement that only runs when the loop terminates naturally (without `break`).
```Python
# Force a loop to terminate?
break

# Skip an iteration of a loop?
continue
```

#### `for` Loops
```Python
# General Syntax
for COUNTER in range(START, END, STEP):       # END excluded
  LOOP_CODE

# Typica Syntax
for COUNTER in range(COUNT):                  # COUNT excluded
  LOOP_CODE
```

#### `while` Loops
```Python
while CONDITION:
  LOOP_CODE
```

### `try-except`
```Python
# General Syntax
try:
  TRY_CODE                              # try to run
except EXCEPTION:  
  EXCEPT_CODE                           # handle a specific exception
...
except (EXCEPTION1, EXCEPTION2, ...):  
  MULTIPLE_EXCEPT_CODE                  # handle multiple specific exceptions
...
else:                                   # runs if no exceptions
  ELSE_CODE
finally:
  FINALLY_CODE                          # always runs

# Raise an exception?
raise EXCEPTION_TYPE("ERROR_MESSAGE")
```

### `pass`
- `pass` is a placeholder used to prevent syntax errors in empty functions, classes, conditionals, or loops.










## Built-In Data Types



### `==` vs `is`




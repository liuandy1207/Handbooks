# <img src=https://cdn.freebiesupply.com/logos/large/2x/python-5-logo-svg-vector.svg width=30px> Python Handbook

## Table of Contents
> ### [Language Details](#language-details) <br>
>> [Commenting](#commenting) <br>

> ### [Variables](#variables) <br>
>> [Local vs Global Variables](#local-vs-global-variables) <br>

> ### [Control Flow](#control-flow) <br>
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

> ### [Built-In Data Types](#built-in-data-types) <br>
>> [Type Casting](#type-casting) <br>
>> [Numeric Data Types and Operators](#numeric-data-types-and-operators) <br>
>> [Boolean Values and Operators](#boolean-values-and-operators) <br>
>> ##### [Iterable Data Types](#iterable-data-types) <br>
>>> [Sequence Data Types](#sequence-data-types) <br>
>>>> [Indexing and Slicing](#indexing-and-slicing) <br>
>>>> [Strings](#strings) <br>
>>>>> [Format Strings](#format-strings) <br>
>>>>
>>>> [Lists](#lists) <br>
>>>>> [Shallow vs Deep Copies a Nested Lists](#shallow-vs-deep-copies-of-nested-lists) <br>
>>>>
>>>> [Tuples](#tuples) <br>
>>> [Sets](#sets) <br>
>>> [Dictionaries](#dictionaries) <br>
>> [`==` vs `is`](#vs-is) <br>









<br>
<br>
<br>
<br>
<br>
<hr>

## Language Details
- Files end with `.py`.

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
- All data types are classes, so all values are objects (instances of a class). 
```Python
# Get the data type of a specific object?
DATA_TYPE = type(OBJECT)
```

### Type Casting
- Each data type has a constructor function that can be used to explicitly convert (cast) data to that type.
```Python
# Cast an object to string?
STRING = str(OBJECT)
```

### Numeric Data Types and Operators
- Python has three numeric data types: `int`, `float`, and `complex`.
- Casting from `float` to `int` risks losing data from truncation.
- You cannot cast from `complex` to `float` or `int`.
```Python
# Define a complex number?
COMPLEX = complex(REAL_PART, IMAGINARY_PART)
COMPLEX = REAL_PART + (IMAGINARY_PART)j

# Define a scientific number?
SCIENTIFIC = (MANTISSA)e(EXPONENT)      # capital E works too

##################################################

# Division
QUOTIENT = DIVIDEND / DIVISOR    # / always returns a float

# Floor Division
QUOTIENT = DIVIDEND / DIVISOR    # // rounds towards negative infinity

# Exponentiation
PRODUCT = BASE ** EXPONENT
```

### Boolean Values and Operators
- `False`, `None`, `0`, and empty strings/lists/tuples/sets/dicts are Falsy, and all other values are Truthy.
```Python
# T/F Syntax
True
False

##################################################

# Boolean AND
RESULT = BOOL1 and BOOL2

# Boolean OR
RESULT = BOOL1 or BOOL2

# Boolean NOT
RESULT = not BOOL
```

### Iterable Data Types
- `str`, `list`, `tuple`, `set`, and `dict` are **iterable data types**.
- Iterable data types allow element-by-element iteration (must implement `__iter__()`).
```Python
# Loop through the elements of an iterable?
for ELEMENT in ITERABLE:
  LOOP_CODE

# Loop through the indicies and elements of an iterable?
for INDEX, ELEMENT in enumerate(ITERABLE):
  LOOP_CODE

# Check if an element is in/not in an iterable?
ELEMENT in ITERABLE
ELEMENT not in ITERABLE

# Get the length of a sized iterable?
LENGTH = len(ITERABLE)
```

### Sequence Data Types
- `str`, `list`, `tuple` are **sequence data types**.
- Sequence data types are ordered and allow indexing and slicing.
```Python
# Sequence Concatenation
NEW_SEQ = SEQ1 + SEQ2 + ...

# Sequence Repetition
NEW_SEQ = SEQ1 * N

# Count the number of instances of a specific element in a sequence?
COUNT = SEQ.count(ELEMENT)

# Get the index of the FIRST instance of a specific element in a sequence?
INDEX = LIST.index(ELEMENT)        # returns ValueError if the element is not found
```

#### Indexing and Slicing
- **Indexing** is the process of accessing elements of a sequence using their position, specified by an integer index.
  - Typical indexing starts at 0, but negative indexing starts at -1. 
- **Slicing** is the process of extracting a subsequence from a sequence.
```Python
# Access the n-th element of a sequence?
ELEMENT = LIST[N-1]        # typical indexing starts at 0

# Access the last element of a sequence?
ELEMENT = LIST[-1]         # negative indexing starts at -1

# Loop through the indices of a sequence?
for INDEX in range(len(SEQ):
  LOOP_CODE

##################################################

# General Syntax for Slicing
SUBSEQ = SEQ[START:END:STEP]

# Slice?
SUBSEQ = SEQ[:END]        # from the start
SUBSEQ = SEQ[START:]      # to the end
SUBSEQ = SEQ[END:START]   # from the end (with negative indexing)

# Construct a new sequence such that it is the reverse a sequence?
NEW_SEQ = SEQ[::-1]

# Replace a subsequence of a MUTABLE sequence with another sequence in-place?
SEQ[SUBSEQ_START:SUBSEQ_END] = OTHER_SEQ

# Construct a new sequence such that a subsequence of an immutable sequence is replaced by another sequence?
NEW_SEQ = SEQ[:SUBSEQ_START] + OTHER_SEQ + SEQ[SUBSEQ_END:]

# Construct a new sequence such that another sequence is inserted at a specific index in a sequence?
NEW_SEQ = SEQ[:INDEX] + OTHER_SEQ + SEQ[INDEX+1:]
```

### Strings
- A **string** is an IMMUTABLE sequence of length 1 strings (no character data type). 
```Python
# Define a string?
STRING = str(VALUE)
STRING = "..."         # or single quotes '

# Define a multi-line string?
STRING = """...
...
..."""                # or triple single quotes '''

# Remove whitespace from the beginning and end of a string?
STRING.strip()

# Convert a string to uppercase/lowercase?
STRING.upper()
STRING.lower()

# Check if a string ends with a specific substring?
STRING.endswith(SUBSTRING)

# Find the index of the FIRST instance of a specific substring in a string?
INDEX = STRING.index(SUBSTRING)       # returns ValueError if the substring is not found
INDEX = STRING.find(SUBSTRING)        # returns -1 if the substring is not found

# Find the index of the LAST instance of a specific substring in a string?
INDEX = STRING.rfind(SUBSTRING)       # returns -1 if the substring is not found

# Split a string into a list of substrings according to a separator character?
LIST_OF_SUBSTRINGS = STRING.split(SEPARATOR)

# Replace all instances of a specific substring with another string?
STRING.replace(SUBSTRING, OTHER_STRING)
```

#### Format Strings
- A **format string** (f-string) is a string that can contain a placeholder (variable or expression).
- Placeholders can have format-specifying modifiers.
```Python
# Define an f-string?
FSTRING = f"...{PLACEHOLDER}..."

# Modify a placeholder to have n decimal points?
FSTRING = f"...{PLACEHOLDER:.Nf}..."
FSTRING = f"...{PLACEHOLDER:.2f}..."      # example: two decimal points

# Modify a placeholder to be a percentage?
FSTRING = f"...{PLACEHOLDER:%}..."

# Modify a placeholder to LEFT/CENTER/RIGHT align within a specific amount of space?
FSTRING = f"...{PLACEHOLDER:<SPACE}..."
FSTRING = f"...{PLACEHOLDER:^SPACE}..."
FSTRING = f"...{PLACEHOLDER:>SPACE}..."
```

### Lists
- A **list** is a mutable sequence of elements.
```Python
# Define a list?
LIST = [ELEMENT1, ELEMENT2, ...]
LIST = list(ELEMENT1, ELEMENT2, ...)

# Add an element to the end of a list?
LIST.append(ELEMENT)

# Insert a specific element at a specific index in a list?
LIST.insert(INDEX, ELEMENT)

# Remove the LAST element of a list?
LIST.pop()

# Remove the element at a specific index in a list?
LIST.pop(INDEX)

# Reverse a list in-place?
LIST.reverse()

# Extend a list by another iterable in-place?
LIST.extend(ITERABLE)

# Sort a list in-place? - Alphanumerically, Increasing
LIST.sort()

# Sort a list in-place? - Alphanumerically, Decreasing
LIST.sort(reverse = True)

# Sort a list in-place using a specific function?
LIST.sort(key = FUNCTION)        # function should a return a number that will be used to sort in increasing order
```

#### Shallow vs Deep Copies of Nested Lists
- A **shallow copy** of a nested list is a new outer list object whose inner elements refer to the same objects as the original.
  - Changes made to MUTABLE elements of a shallow copy will affect the original and vice-versa. 
- A **deep copy** of a nested list does not refer to any objects shared with the original.
   - Changes made to a deepy copy will NOT affect the original and vice-versa. 
```Python
# Make a shallow copy of a nested list?
COPY = ORIGINAL[:]
COPY = ORIGINAL.copy()

# Make a deep copy of a nested list?
"""
1. Directly copy IMMUTABLE inner elements.
2. Recursively make copies of MUTABLE inner elements.
"""
```





### `==` vs `is`




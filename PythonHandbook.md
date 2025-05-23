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
>> #### [Iterable Data Types](#iterable-data-types) <br>
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

> ### [Functions](#functions) <br>
>> [Positional and Keyword Arguments](#positional-and-keyword-arguments) <br>
>> [Docstrings](#docstrings) <br>
>> [Annotations](#annotations) <br>

> ### [Modules](#modules) <br>






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
- A **variable** is an identifier that refers to a value (object) in memory.
- Variables are **dynamically typed** => a variable takes on the type of the value (object) it refers to at runtime.
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
- Sequence data types are ordered iterables and allow indexing and slicing.
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
INDEX = STRING.index(SUBSTRING)       # returns ValueError if SUBSTRING not in STRING
INDEX = STRING.find(SUBSTRING)        # returns -1 if SUBSTRING not in STRING

# Find the index of the LAST instance of a specific substring in a string?
INDEX = STRING.rfind(SUBSTRING)       # returns -1 if SUBSTRING not in STRING

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
LIST.sort(key = FUNCTION)        # FUNCTION should return a value that will be used to sort in increasing order
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

### Tuples
- A `tuple` is an immutable sequence of elements. 
```Python
# Define a tuple?
TUPLE = (ELEMENT1, ELEMENT2, ...)
TUPLE = tuple(ELEMENT1, ELEMENT2, ...)

# Define a tuple with one element?
TUPLE = (ELEMENT,)
TUPLE = tuple(ELEMENT)

# Modify a tuple?
TUPLE_AS_LIST = list(TUPLE)      # convert to a mutable list
...                              # modify the tuple as a list
TUPLE = tuple(TUPLE_AS_LIST)     # convert back to an immutable tuple
```

### Sets
- A set is an unordered iterable of unique immutable elements.
  - The order of iteration is random.
- Sets do NOT allow duplicate elements.
  - `True` & `1` and `False` & `0` are considered duplicates.
```Python
# Define a set?
SET = {ELEEMNT1, ELEMENT2, ...}
SET = set(ELEMENT1, ELEMENT2, ...}

# Add an element to a set?
SET.add(ELEMENT)

# Merge multiple sets into a single set?
SET.update(SET1, SET2, ...)

# Remove a random element of a set?
SET.pop()

# Remove a specific element of a set?
SET.remove(ELEMENT)         # raises ValueError if ELEMENT not in SET
SET.discard(ELEMENT)        # no effect if ELEMENT not in SET

# Check if a set is a SUBSET of another set?
SET.issubset(OTHER_SET)

# Check if a set is a SUPERSET of another set?
SET.issuperset(OTHER_SET)

# Check if two sets are disjoint?
SET1.isdisjoint(SET2)

# Set Union
SET.update(ITER1, ITER2, ...)                  # modifies in-place
NEW_SET = SET.union(ITER1, ITER2, ...)         # iterable must contain immutable elements only
NEW_SET = SET1 | SET2 | ...
SET |= OTHER_SET

# Set Intersection
SET.intersection_update(ITER1, ITER2, ...)       # modifies in-place
NEW_SET = SET.intersection(ITER1, ITER2, ...)    # ITER1, ITER2, ... must contain immutable elements only
NEW_SET = SET1 & SET2 & ...
SET &= OTHER_SET

# Set Difference
SET.difference_update(ITER1, ITER2, ...)       # modifies in-place
NEW_SET = SET.difference(ITER1, ITER2, ...)    # ITER1, ITER2, ... must contain immutable elements only
NEW_SET = SET1 - SET2 - ...
SET -= OTHER_SET

# Set Symmetric Difference
SET.symmetric_difference_update(ITER1, ITER2, ...)       # modifies in-place
NEW_SET = SET.symmetric_difference(ITER1, ITER2, ...)    # ITER1, ITER2, ... must contain immutable elements only
NEW_SET = SET1 ^ SET2 ^ ...
SET ^= OTHER_SET
```

### Dictionaries
- A **dictionary** is an iterable of key:value pairs.
- Keys must be unique and immutable, but values can be repeated and mutable.
- Equality operators (`==` and `!=`) disregard order for dictionaries. 
```Python
# Define a dictionary?
DICT = {KEY1:VAL1, KEY2:VAL2, ...}
DICT = dict(KEY1:VAL1, KEY2:VAL2, ...)

# Construct a dictionary from two sequences?
DICT = dict(zip(KEY_SEQ, VAL_SEQ))

# Construct a dictionary from an iterable of keys and the same default value?
DICT = dict.fromkeys(ITERABLE, DEFAULT)

# Merge multiple dictionaries into a single dictionary?
DICT.update(DICT1, DICT2, ...)         # DICT1, DICT2, ... kvps overwrite DICT kvps

# Construct a new dictionary that is the combination of multiple dictionaries?
NEW_DICT = DICT1 | DICT2 | ...      # right-side dict keys overwrite left-side dict keys
DICT |= OTHER_DICT

# Add a key:value pair to a dictionary?
DICT[KEY] = VALUE

# Access the value associated with a specific key in a dictionary?
VALUE = DICT.get(KEY)         # returns the default value if KEY not in DICT
VALUE = DICT[KEY]             # raises KeyError if KEY not in DICT

# Set a specific default value for a key?
VALUE = DICT.setdefault(KEY, DEFAULT)      # if KEY in DICT, return VALUE
                                           # if KEY not in DICT, insert KEY:DEFAULT and return DEFAULT

# Access the value associated with specific keys in a NESTED dictionary?
VALUE = [OUTER_KEY][INNER_KEY]

# Remove the LAST element of a dictionary?
DICT.popitem()

# Remove the element associated with a specific key in a dictionary?
VALUE = DICT.pop(KEY)            # returns the removed value, raises KeyError if KEY not in DICT
VALUE = DICT.pop(KEY, DEFAULT)   # returns the remove value, returns DEFAULT if KEY not in DICT
del DICT[KEY]

# Empty a dictionary in-place?
DICT.clear()

# Construct a list of KEYS of a dictionary?
KEYS = DICT.keys()            # KEYS will change if DICT changes

# Construct a list of VALUES of a dictionary?
VALUES = DICT.values()        # VALUES will change if DICT changes

# Construct a list of KEY:VALUE PAIRS of a dictionary?
KVPS = DICT.items()           # KVPS will change if DICT changes
                              # each key:value pairs is a tuple

# Loop through the keys and values of a dictionary?
for KEY, VALUE in DICT.items():
  LOOP_CODE

# Check if a specific KEY is in a dictionary?
KEY in DICT

# Check if a specific VALUE is in a dictionary?
VAL in DICT.values()
```

### `==` vs `is`
- `==` checks if two objects have the same value.
- `is` checks if two variables refer to the exact same object.
  - Use `is` to compare objects to `None`. 








## Functions
- Python uses **pass-by-object-reference** => when an object is passed to a function, a parameter becomes a reference to the passed object.
  - If the passed object is immutable, then the original object cannot be affected by the function since reassignments create new local objects.
  - If the passed object is mutable, then in-place modifications will affect the original object.
```Python
# Define a function?
def FUNCTION(PARAM1, PARAM2, ...):
  FUNCTION_CODE
  return VALUE            # optional, returns None if not specified

# Return multiple values (objects) in a function?
return VALUE1, VALUE2, ...            # packed as a tuple

# Define a function with default parameters?
def FUNCTION(PARAM1 = DEFAULT1, PARAM2 = DEFAULT2, ...):
  FUNCTION_CODE
```

### Positional and Keyword Arguments
- A **parameter** is a (local) variable in a function's definition.
- An **argument** is a value (object) passed to a function parameter in a call.
  - A **positional argument** is an argument that is matched to a parameter based on its position in the function call.
  - A **keyword argument** is an argument that is matched to a specific parameter by name (order does NOT matter).
- Calling a function with positional AND keyword arguments requires that all positional arguments come before any keyword arguments. 
```Python
# Define a function that takes arbitary positional arguments?
def FUNCTION(..., *PARAM, ...):     # *PARAM takes a tuple of arguments such that
  FUNCTION_CODE                     # params left = args left

# Define a function that takes arbitary keyword arguments?
def FUNCTION(..., **PARAM, ...):    # *PARAM takes a dictionary of arguments such that
  FUNCTION_CODE                     # params left = args left

# Define a function to take positional-only or keyword-only arguments?
def FUNCTION(POS_ONLY, ..., /, ..., POS_OR_KW, ..., * KW_ONLY_PARAM, ...):
  FUNCTION_CODE                     # parameters BEFORE / are positional-only
                                    # parameters AFTER * are keyword-only

# Call a function through positional arguments?
FUNCTION(ARG1, ARG2, ...)
FUNCTION(*TUPLE)                    # tuple unpacking

# Call a function through keyword arguments?
FUNCTION(PARAM1 = ARG1, PARAM2 = ARG2, ...)
FUNCTION(**DICT)                    # dictionary unpacking
```

### Docstrings
- A **docstring** of a function is a string literal in the first statement of a function's definition that supplies documentation for the function.
- Docstrings are written in the imperative. 
```Python
def FUNCTION():
  """ Does something """
```

### Annotations
- An **annotation** is optional metadata attached to a function parameter or return value.
- Annotations are often used indicate the expected type of a function's parameters and return value, but do not enforce any restrictions on the function. 
```Python
# Include annotations for a function?
def FUNCTION(PARAM1: TYPE, PARAM2: TYPE, ...) -> RETURN_TYPE:
  FUNCTION_CODE
  return VALUE

# Include annotations and default values for a function?
def FUNCTION(PARAM1: TYPE = DEFAULT1, PARAM2: TYPE = DEFAULT2, ...) -> RETURN_TYPE:
  FUNCTION_CODE
  return VALUE
```









## Modules
- A **module** is a Python file that is imported to a script.
- A **name** is an identifier that refers to an object.
  - All variables are names, but not all names are variables. Some names are identifiers for functions, classes, modules, etc. 
```Python
# Import a module?
import MODULE

# Import a module with renaming?
import MODULE as M

# Import a specific name from a module?
from MODULE import NAME

# Import all names from a module?
from MODULE import *

# Call a function from a module?
MODULE.FUNCTION()

# List all names in the current scope?
dir()
```














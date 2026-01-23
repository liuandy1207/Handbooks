# <img src=https://cdn.freebiesupply.com/logos/large/2x/python-5-logo-svg-vector.svg width=30px> Python Handbook

## Table of Contents
> ### [Language Details](#language-details) <br>
>> [Indentation and Scope](#indentation-and-scope) <br>
>> [Comment Syntax](#comment-syntax) <br>
>> [Multi-Line Statements](#multi-line-statements) <br>
>> [Identifiers](#identifiers) <br>

> ### [Variables](#variables) <br>
>> [Local vs Global Variables](#local-vs-global-variables) <br>
>> [`==` vs `is`](#-vs-is) <br>

> ### [Control Flow](#control-flow) <br>
>> [Main Function](#main-function) <br>
>> [`if-elif-else` Statements](#if-elif-else-statements) <br>
>> [`match-case` Structures](#match-case-structures) <br>
>> [Loops](#loops) <br>
>>> [`for` Loops](#for-loops) <br>
>>> [`while` Loops](#while-loops) <br>
>>
>> [`try-except` Structures](#try-except-structures) <br>

> ### [Data Types](#data-types) <br>
>> [Type Casting](#type-casting) <br>
>> [Numeric Data Types](#numeric-data-types) <br>
>> [Boolean Values](#boolean-values) <br>
>> #### [Collection Data Types](#collection-data-types) <br>
>>> [Sequence Data Types](#sequence-data-types) <br>
>>>> [Slicing](#slicing) <br>
>>>> [Strings](#strings) <br>
>>>>> [Format Strings](#format-strings) <br>
>>>>
>>>> [Lists](#lists) <br>
>>>>> [List Comprehension](#list-comprehension) <br>
>>>>> [Shallow vs Deep Copies of Nested Lists](#shallow-vs-deep-copies-of-nested-lists) <br>
>>>>
>>>>[Tuples](#tuples) <br>
>>>
>>> [Sets](#sets) <br>
>>> [Dictionaries](#dictionaries) <br>

> ### [Functions](#functions) <br>
>> [Lambda Functions](#lambda-functions) <br>





















<br>
<br>
<br>
<hr>

## Language Details
- Python scripts end in `.py`.

### Indentation and Scope
- Indentation must be equal within the same suite/block since indentation defines scope.

### Comment Syntax
```Python
# this is a comment

"""
this is
a multi-line
string literal
which can be used
as a multi-line comment
"""
```

### Multi-Line Statements
- New lines terminate statements, but `\` continues a statement onto the next line.
  - Elements contained within any brackets can continue onto the next line without using `\`.
```Python
# Continue a statement onto the next line?
# expression example
x = 1 + \
    2 + \
    3

# elements example
x = [1,
     2,
     3]          # brackets example
```

### Identifiers
- An **identifier** is a symbolic name for a variable, function, class, module, or other object.

<br>

- Identifers must begin with a letter or `_`. Identifers can contain letters, numbers, or `_`.
- By convention:
  - Starting with `_` indicates that the identifier is **private**.
  - Starting AND ending with `__` indicates that the identifer is a special Python method (**dunder method**).
  - Variable identifers use `snake_case`.




<hr>

## Variables
- A **variable** is an identifer that refers to a value in memory.
  - An expression is a statement that evaluates to a value.
 
<br>

- Variables are **dynamically typed** => Variables take on the type of the values they refer to at runtime.
```Python
# Assign a value (or expression) to a variable?
VARIABLE = VALUE

# Assign one value to multiple variables?
VAR1 = VAR2 = ... = VALUE

# Swap the values of two variables?
VAR1, VAR2 = VAL2, VAL1

# Assign multiple values (or expressions) to multiple variables?
VAR1, VAR2, ... = VAL1, VAL2, ...

# NOTE TO SELF: move to section on iterables because iterabls can unpack, also do a note on packing variables
# Unpack a tuple into variables? 
(VAR1, VAR2, ...) = TUPLE        # if * precedes a variable
                                 # then values will fill that variable until
                                 # the number of values left = the number of variables left
```

### Local vs Global Variables
- A **local variable** is a variable that is defined (and accessible) within a function.
- A **global variable** is a variable that is defined (and accessible) in the main body.

<br>

- Variables are accessible in the scope they are defined in.
  - A local variable with the same name as a global variable has priority.
    - Declaring a local variable as global will raise a `SyntaxError`.
- For functions:
  - Parameters are local variables.
  - Global variables must be explicitly declared `global` before assignment.
  - For the inner function of a nested function, variables in the scope of the outer function must be explicitly declared `nonlocal` before assignment.

```Python
# Declare a variable to be global?
global VARIABLE

# List global identifers?
dir()

# Declare a variable to be nonlocal?
nonlocal VARIABLE

```

### `==` vs `is`
- `==` checks if two objects have the same value. 
- `is` checks if two variables refer to the exact same object.
  - Use `is` to compare objects to `None`.





<hr>

## Control Flow
- Control flow is the order in which statements are executed in a script. 

### Main Function
- A **main function** is a function that acts as a script's **entry point** when it is run directly. It is NOT run when imported

<br>

- When a script is run directly, `__name__` is set to `"__main__"`.
- When a module is imported `__name__` is set to the name of the module.
```Python
# Define a main function?
if __name__ "__main__":
  MAIN_BODY_CODE
```

### `if-elif-else` Statements
```Python
# General Case
if IF_CONDITION:
  IF_CODE
elif ELIF1_CONDITION:
  ELIF1_CODE
elif ELIF2_CONDITION:
  ELIF2_CODE
...
else:
  ELSE_CODE

# Ternary Operator
IF_CODE if CONDITION else ELSE_CODE

# Shorthand If Statement
if CONDITION: CODE
```

### `match-case` Structures
- `match` and `case` are **soft keywords** => They are only keywords in the match-case structure.
```Python
# General Cases
match EXPRESSION:
  case VALUE1:
    CASE_CODE
  case VALUE2:
    CASE_CODE
  ...
  # Give a case multiple values?
  case VALUE1 | VALUE2 | ...:
    CASE_CODE
  # Give a case an extra condition to check?
  case VALUE if CONDITION:
    CASE_CODE
  # Define a default case?
  case _:
    DEFAULT_CODE

# List Expression Cases
match LIST:
  # Match each element exactly?
  case [ELEMENT1, ELEMENT2, ...]:    # position matters
    CASE_CODE
  # Ignore matching for some indices?
  case [_, _, ..., ELEMENT, _, _, ...]:    # use _ as a wildcard element
    CASE_CODE
  # Match an arbitrary number of elements?
  case [..., *REST, ...]:        # the variable preceeded by * will take on enough elements such that
    CASE_CODE                    # elements left in the list = elements left in the case
                                 # * can only appear once in a case
```

### Loops
- `for` and `while` loops can have an additional `else` statement that only runs when the loop terminates naturally without `break`.
```Python
# Force a loop to terminate?
break

# Skip an iteration of a loop?
continue

# Create a code stub (placeholder code)?
pass

```

#### `for` Loops
- `for` loops can directly iterate over any iterable.
  - It is unsafe to add/remove elements from an iterable while iterating over it.
  - Modifying the loop variable will NOT affect the original iterable.
```Python
# Typical Case
for COUNTER in range(COUNT):
  LOOP_CODE

# General Case
for COUNTER in range(START, END, STEP):
  LOOP_CODE

# Iterable Case - by Element
for ELEMENT in ITERABLE:
  LOOP_CODE

# Iterable Case - by Index and Element
for INDEX, ELEMENT in enumerate(ITERABLE):      # enumerate() returns a tuple
  LOOP_CODE

# Change the starting index of enumerate()?
enumerate(ITERABLE, start=START)
```

#### `while` Loops
- `while` loops are best for:
  - Looping for an unknown amount of iterations,
  - Removing items from an iterable,
  - Getting user input, and
  - Event loops.
```Python
# General Case
while CONDITION:
  LOOP_CODE
```

### `try-except` Structures
```Python
# General Case
try:
  TRY_CODE        # potentially raises an exception
except (EXCEPTION1, EXCEPTION2, ...):
  EXCEPT_CODE     # handles the stated exceptions
else:
  ELSE_CODE       # executes if no exceptions have been raised
finally:
  FINALLY_CODE    # always executes, regardless of any exceptions or lack thereof

# Handle every type of exception?
except:    
  EXCEPT_CODE     # bad practice to not explicitly specify an exception type

# Ignore an exception?
except EXCEPTION:
  pass

# Raise an exception?
raise Exception("ERROR_MESSAGE")        # general case
raise EXCEPTION_TYPE("ERROR_MESSAGE)    # specific case

# Assert that a condition is met?
assert CONDITION, "ERROR_MESSAGE"      # raises AssertionError if CONDITION is False
                                       # should only be used for debugging

```




<hr>

## Data Types
- Everything in Python is an object, and all objects are instances of a class.
- `int`, `float`, `complex`, `bool`, `str`, and `NoneType` are **primitive data types** => They are the most fundamental data types because they hold single values and do not contain other objects.

### Type Casting
- Since each data type is a class, each data type has a constructor function that can be used explicitly convert (cast) data to that type. 
```Python
# Get the data type of a specific value?
DATA_TYPE = type(VALUE)

# Cast a specific value to a string?
STRING = str(VALUE)
```

### Numeric Data Types
- Python has 3 built-in numeric data types: `int`, `float`, and `complex`.

<br>

- There is no pre-defined integer limit in Python. 
- Casting from a `float` to `int` risks losing data by truncation.
- You CANNOT cast from `complex` to `float` or `int`.
```Python
# Define a complex number?
COMPLEX = complex(REAL_PART, IMAGINARY_PART)    # constructor function
COMPLEX = REAL_PART + IMAGINARY_PARTj
c = 2 + 2j                                      # example  

# Define a scientific number?
SCIENTIFIC_NUM = MANTISSAeEXPONENT        # capital E works tooo
avagadro = 6.022e23                       # example

# Perform division?
QUOTIENT = DIVIDEND / DIVISOR       # / always returns a float

# Perform floor division?
QUOTIENT = DIVIDEND // DIVISOR      # // rounds towards negative infinity

# Perform exponentiation?
PRODUCT = BASE**EXPONENT
```

### Boolean Values
- `None`, `0`, and empty strings/lists/tuples/dicts/sets are `False` (Falsy), and all other values are `True` (Truthy).
- Boolean logic operators cast `int`s to `bool`s for comparison, but return the original `int` values.
```Python
# Constructor Function?
bool()

# T/F Syntax
True
False

# Boolean AND Syntax
BOOL1 and BOOL2

# Boolean OR Syntax
BOOL1 or BOOL2

# Negate a Boolean value?
not BOOL
```

## Collection Data Types
- `str`, `list`, `tuple`, `set`, and `dict` data types are **collection data types** => They are sized, iterable objects that hold references to other objects (elements).
- `list`, `tuple`, `set`, and `dict` can contain any data type, even different data types. 
```Python
# Loop through the elements of a COLLECTION?
for ELEMENT in COLLECTION:
  LOOP_CODE

# Loop through the indices and elements of an collection?
for INDEX, ELEMENT in COLLECTION:
  LOOP_CODE

# Check if an element is in an collection?
ELEMENT in COLLECTION

# Check if an element is NOT in an collection?
ELEMENT not in COLLECTION

# Get the length of a collection?
LENGTH = len(COLLECTION)

```

### Sequence Data Types
- `str`, `list`, and `tuple` data types are **sequence data types** => They are ordered collections.
- Sequences support indexing and slicing. 
```Python
# Concatenate multiple sequences of the SAME TYPE into a new sequence?
NEW_SEQ = SEQ1 + SEQ2 + ...

# Construct a new sequence that is a sequence repeated n times?
NEW_SEQ = SEQ * N

# Count the number of instances of an element in a sequence?
COUNT = SEQ.count(ELEMENT)      # works with substrings

# Get the index of the FIRST instance of a specific element in a sequence?
INDEX = LIST.index(ELEMENT)     # returns ValueError if the element is not found

# Access the n-th element of a sequence?
ELEMENT = LIST[N]          # indexing (starts at 0)

# Access the last element of a sequence?
ELEMENT = LIST[-1]         # negative indexing (starts at -1)

# Loop through the  indices of a sequence?
for INDEX in range(len(SEQUENCE):
  LOOP_CODE
```

#### Slicing
- **Slicing** is a method of extracting a subsequence from a sequence.
- Standard indexing starts at 0, but negative indexing starts at -1. 
```Python
# Slice from a starting index to an ending endex?
SUBSEQ = SEQ[START:END]]

# Slice from the start?
SUBSEQ = SEQ[:END]

# Slice to the end?
SUBSEQ = SEQ[START:]

# Slice with a non-default step?
SUBSEQ = SEQ[START:END:STEP]

# Slice from the end?
SUBSEQ = SEQ[END:START]      # indices would be NEGATIVE

# Construct a new sequence that is the reverse of a sequence?
NEW_SEQ = SEQ[::-1]

# Slice to replace a subsequence of a MUTABLE sequence in-place?
SEQ[SUBSEQ_START:SUBSEQ_END] = OTHER_SEQ

# Slice to construct a new sequence where a subsequence of a sequence is replaced with another sequence?
NEW_SEQ = SEQ[:SUBSEQ_START] + OTHER_SEQ + SEQ[SUBSEQ_END:]      # works with IMMUTABLE sequences

# Slice to construct a new sequence where another sequence is inserted at a specific index in a sequence?
NEW_SEQ = SEQ[:INDEX] + OTHER_SEQ + SEQ[INDEX+1:]                # works with IMMUTABLE sequences
```

#### Strings
- A **string** is an immutable sequence of characters.

<br>

- There is no "character" data type in Python, so each character/element is a string of length 1.
```Python
# Define a string?
STRING = str(VALUE)    # constructor function
STRING = "..."         # or single quotes '

# Define a multi-line string?
STRING = """ ...
...
... """                   # or triple single quotes '''

# Remove whitespace from the beginning and end of a string?
STRING.strip()

# Convert a string to uppercase/lowercase?
STRING.upper()
STRING.lower()

# Check if a string is entirely whitespace?
STRING.isspace()          # there are many similar functions for different character types

# Check if a string ends with a specific substring?
STRING.endswith(SUBSTRING)

# Find the index of the FIRST/LAST instance of a specific substring in a string?
STRING.find(SUBSTRING)        # returns -1 if the substring is not found
STRING.rfind(SUBSTRING)

# Split a string into a list of substrings according to a specific separator character?
LIST_OF_SUBSTRINGS = STRING.split(SEPARATOR)

# Replace all instances of a specific substring another specific substring?
STRING.replace(REPLACED_STRING, REPLACING_STRING)
```

#### Format Strings
- A **format string** (f-string) is a string that can contain a placeholder variable or expression.

<br>

- Placeholders in f-strings can have format-specifying modifiers.
```Python
# Define an f-string?
FSTRING = f"...{PLACEHOLDER}..."

# Choose a placeholder conditionally?
FSTRING = f"...{IF_PLACEHOLDER if CONDITION else ELSE_PLACEHOLDER}..."

# Modify a placholder to have n decimal points?
FSTRING = f"...{PLACEHOLDER:.Nf}..."
FSTRING = f"...{PLACEHOLDER:.2f}..."      # example to two decimal points

# Modify a placeholder to be in scientific format?
FSTRING = f"...{PLACEHOLDER:.e}..."
FSTRING = f"...{PLACEHOLDER:.E}..."

# Modify a placeholder to be a percentage?
FSTRING = f"...{PLACEHOLDER:%}..."

# Modify a placeholder to left/center/right align within a specific amount of space?
FSTRING = f"...{PLACEHOLDER:<SPACE}..."
FSTRING = f"...{PLACEHOLDER:^SPACE}..."
FSTRING = f"...{PLACEHOLDER:>SPACE}..."
```

#### Lists
- A **list** is a mutable sequence of elements.
```Python
# Define a list?
LIST = [ELEMENT1, ELEMENT2, ...]
LIST = list(ELEMENT1, ELEMENT2, ...)      # constructor function
LIST = list(COLLECTION)

# Add an element to the end of a list?
LIST.append(ELEMENT)

# Insert a specific element at a specific index of a list?
LIST.insert(INDEX, ELEMENT)

# Remove the FIRST instance of a specific element from a list?
LIST.remove(ELEMENT)        # raises ValueError if the element is not found

# Remove the LAST element of a list?
LIST.pop()

# Remove the element at a specific index from a list?
LIST.pop(INDEX)

# Reverse a list in-place?
LIST.reverse()

# Extend a list by another list?
LIST.extend(OTHER_LIST)        # works with any iterable

# Sort a list? - Alphanumerically, Increasing
LIST.sort()

# Sort a list? - Alphanumerically, Decreasing
LIST.sort(reverse = True)

# Sort a list using a specific function?
LIST.sort(key = FUNCTION)      # function must return a number that will be used to sort in increasing order
```

#### List Comprehension
- **List comprehension** is a method of constructing new lists using the elements of a list.
```Python
# General Case
NEW_LIST = [EXPRESSION for ELEMENT in LIST if CONDITION]

# Filter Case
NEW_LIST = [ELEMENT for ELEMENT in LIST if CONDITION]

# Mapping Case
NEW_LIST = [EXPRESSION for ELEMENT in LIST]
```

#### Shallow vs Deep Copies of Nested Lists
- A **shallow copy** of a nested list creates a new outer list, but inner elements are still references to the same objects as in the original.
  - Changes made to MUTABLE inner elements (lists) will affect both the copy and the original.
- A **deep copy** of a nested list creates a completely independent copy of the original such that no references refer to the same objects. 
  - Changes made to the copy will NOT affect the original, and vice versa. 
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

#### Tuples
- A **tuple** is an immutable sequence of elements.
```Python
# Define a tuple?
TUPLE = (ELEMENT1, ELEMENT2, ...)
TUPLE = tuple(ELEMENT1, ELEMENT2, ...)      # constructor function
TUPLE = tuple(COLLECTION)

# Define a tuple with one element?
TUPLE = tuple(ELEMENT)
TUPLE = (ELEMENT,)

# Modify a tuple?
TUPLE_AS_LIST = list(TUPLE)      # convert to a mutable list
...                              # modify the tuple as a list
TUPLE = tuple(TUPLE_AS_LIST)     # convert back to an immutable tuple
```

#### Sets
- Sets are unordered collections of IMMUTABLE elements.

<br>

- Sets do NOT allow duplicate elements.
  - `True` & `1` and `False` & `0` are consisdered duplicates.
- Sets operate on hash tables, so membership checking is very fast.
- Sets are best when duplicates do not need to be stored.
- The order of iterating through a set is random. 
```Python
# Define a set?
SET = {ELEMENT1, ELEMENT2, ...}
SET = set(ELEMENT1, ELEMENT2, ...)       # constructor function
SET = set(COLLECTION)                    # collection must contain immutable elements only

# Add an element to a set?
SET.add(ELEMENT)

# Add the elements of multiple sets to a set?
SET.update(SET1, SET2, ...)

# Remove a RANDOM element from a set?
SET.pop()

# Remove a specific element from a set?
SET.remove(ELEMENT)         # raises ValueError if the element is not found
SET.discard(ELEMENT)        # does NOT raise any exceptions if the element is not found

# Check if a set is a SUBSET of another set?
SET.issubset(OTHER_SET)

# Check if a set is a SUPERSET of another set?
SET.issuperset(OTHER_SET)

# Check if two sets are disjoint?
SET1.isdisjoint(SET2)

# Modify a set to be the UNION of the set with other sets in-place?
SET.update(SET1, SET2, ...)      # works with any iterables
SET |= OTHER_SET                 # only works with one other set

# Construct a new set that is the UNION of multiple sets?
NEW_SET = SET1 | SET2 | ...      # only works with sets
NEW_SET = SET1.union(SET2, ...)  # works with any iterables

# Modify a set to be the INTERSECTION of the set with other sets in-place?
SET.intersection_update(SET1, SET2, ...)      # works with any iterables
SET &= OTHER_SET                              # only works with one other set

# Construct a new set that is the INTERSECTION of multiple sets?
NEW_SET = SET1 & SET2 & ...               # only works with sets
NEW_SET = SET1.intersection(SET2, ...)    # works with any iterables

# Modify a set to be the DIFFERENCE of the set with other sets in-place?
SET.difference_update(SET1, SET2, ...)      # works with any iterables
SET -= OTHER_SET                            # only works with one other set

# Construct a new set that is the DIFFERENCE of multiple sets?
NEW_SET = SET1 - SET2 - ...             # only works with sets
NEW_SET = SET1.difference(SET2, ...)    # works with any iterables

# Modify a set to be the SYMMETRIC DIFFERENCE of the set with other sets in-place?
SET.symmetric_difference_update(SET1, SET2, ...)      # works with any iterables
SET ^= OTHER_SET                                      # only works with one other set

# Construct a new set that is the SYMMETRIC DIFFERENCE of multiple sets?
NEW_SET = SET1 ^ SET2 ^ ...                       # only works with sets
NEW_SET = SET1.symmetric_difference(SET2, ...)    # works with any iterables
```

#### Dictionaries
- Dictionaries are collections of key:value pairs.

<br>

- Keys must be unique and immutable (hashable), but values can be repeated and mutable. 
- Keys are like indices for dictionaries.
```Python
# Define a dictionary?
DICT = {KEY1:VAL1, KEY2:VAL2, ...}
DICT = dict(KEY1:VAL1, KEY2:VAL2, ...)      # constructor function
DICT = dict(COLLECTION)                     # collection must contain key:value pair tuples only

# Access the value associated with a specific key in a dictionary?
VALUE = DICT.get(KEY)        # returns None if the key is not found
VALUE = DICT[KEY]            # raises KeyError if the key is not found

# Access the value associated with specific keys in a NESTED dictionary?
VALUE = DICT[OUTER_KEY][INNER_KEY]

# Remove the LAST element of a dictionary?
DICT.popitem()

# Remove the element associated with a specific key in a dictionary?
DICT.pop(KEY)

# Construct a list of KEYS of a dictionary?
KEYS = DICT.keys()            # the list will change if the dictionary changes

# Construct a list of VALUES of a dictionary?
VALUES = DICT.values()        # the list will change if the dictionary changes

# Construct a list of KEY:VALUE PAIRS of a dictionary?
KVPS = DICT.items()           # the list will change if the dictionary changes
                              # key:value pairs are stored as TUPLES in the list

# Loop through the keys and values of a dictionary?
for KEY, VALUE in DICT.items():
  LOOP_CODE

# Check if a specific KEY is in a dictionary?
KEY in DICT

# Check if a specific VALUE is in a dictionary?
VAL in DICT.values()

# Merge multiple dictionaries into one dictionary?
DICT.update(DICT1, DICT2, ...)
```




<hr>

## Functions
- A **function** is a reusable block of code that performs a specific task.

<br>

- Functions can take inputs (parameters) and optionally return a value.





















































shujpoujipjoijpoijpoijpoijopijpoi
<hr>
<hr><hr>
<hr>
<hr>
<hr>
<hr>
<hr>
<hr>
<hr>
<hr>

<hr>
<hr>
<hr>

<hr>

### Functions
- Functions are first-class citizens.

```Python
# Define a function?
def FUNCTION(PARAM1, PARAM2, ...):
  FUNCTION_CODE
  return RETURN_VALUE        # optional

# Call a function?
FUNCTION(ARG1, ARG2, ...)

# Return multiple values?
return VALUE1, VALUE2, ...    # returns a tuple of values

```

<hr>

### Docstrings
- Docstrings are multi-line strings that describes a function's purpose, located under the function's signature.

> Written in the imperative.

```Python
def FUNCTION(PARAM1, PARAM2, ...):
  """
  DOCSTRING
  """
  FUNCTION_CODE 

```

<hr>

### Parameters vs Arguments
- **Parameters**: local variables defined in a function signature
- **Arguments**: values passed to a function during a call

<hr>

### Positional Arguments, Keyword Arguments, and Arbitrary Arguments
- **Positional Arguments**: arguments passed to a function without explicitly naming the parameters (in the order of the function signature)
  - **Arbitrary Positional Arguments**: when a function accepts any number of positional arguments, packed as a TUPLE

- **Keyword Arguments (kwargs)**: arguments passed to a function by explicitly naming the parameters (order does NOT matter)
  - **Arbitrary Keyword Arguments**: when a function accepts any number of keyword arguments, packed as a DICTIONARY

```Python
# Call a function with keyword arguments?
FUNCTION(PARAM = ARG, ...)    # order does NOT matter

# Define a function with default parameter values?
def FUNCTION(PARAM1 = DEFAULT1, PARAM2 = DEFAULT2, ...):
  FUNCTION_CODE

# Define a function with arbitrary positional arguments?
def FUNCTION(*PARAMS):      # receives a TUPLE of arguments
  FUNCTION_CODE

# Define a function with arbitrary keyword arguments?
def FUNCTION(**PARAMS):     # receives a DICTIONARY of arguments
  FUNCTION_CODE

# Force a function parameter to only accept positional arguments?
def FUNCTION(POS_PARAM, /, ...):    # put , / AFTER any positional-argument-only parameter
  FUNCTION_CODE

# Force a function parameter to only accept keyword arguments?
def FUNCTION(*, KW_PARAM, ...):    # put * , BEFORE any kwarg-only parameter
  FUNCTION_CODE

```

<hr>

### Lambda Functions
- Lambda Functions are small anonymous functions that can take any number of arguments, but can only have one expression.

```Python
# Define a lambda function?
LAMBDA_FUNCTION = lambda PARAM1, PARAM2, ...: EXPRESSION
x = lambda a, b: a * b  # example

```

<hr>

### User Input
- It is good practice to validate any user input using try-except to check if the user provides valid input.

```Python
# Get user input from console?
INPUT = input(PROMPT_STRING)     # Python stops executing and waits for input before continuing
                                 # PROMPT_STRING is optional
                                 # INPUT is a string

```

<hr>

### Classes
- Classes are object constructors.
- Class identifers start with an uppercase letter. 
- Classes can have attributes (variables) and methods (functions). 
- The `self` parameter of a instance method is a reference to the current instance of a class.
  - Used to access variables that belong to the class / object.
  - Can be named anything, but has to be the FIRST PARAMETER of any instance method.

```Python
# Define a class?
class CLASS:
  CLASS_ATTRIBUTE = VALUE      # shared by all instances of the class
  ...
  def __init__(self, ATTRIBUTE1, ATTRIBUTE2, ...):
    self.ATTRIBUTE1 = ATTRIBUTE1
    self.ATTRIBUTE2 = ATTRIBUTE2      # convention to name hidden attributes with a leading _
    ...

  def INSTANCE_METHOD(self):      # self must be the first parameter
    INSTANCE_METHOD_CODE
  ...
  @classmethod      # class methods are shared by all instances
  def CLASS_METHOD(CLASS):        # CLASS must be the first argument
    CLASS_METHOD_CODE
  ...
  @staticmethod     # static methods are called without class/instance reference
  def STATIC_METHOD():
    STATIC_METHOD_CODE
  ...
  @property            # getter function, makes ATTRIBUTE read-only
  def ATTRIBUTE(self):
    return self.ATTRIBUTE
  @ATTRIBUTE.setter    # setter functino, allows ATTRIBUTE to be set
  def ATTRIBUTE(self, ATTRIBUTE):
    self.ATTRIBUTE = ATTRIBUTE

# Define a class with no content?
class CLASS:
  pass            # useful for child classes in inheritance

# Create an instance of a class?
INSTANCE = CLASS()

# Delete an instance of a class?
del INSTANCE

# Modify an attribute of an instance?
INSTANCE.ATTRIBUTE = VALUE

# Delete a attribute of an object?
del INSTANCE.ATTRIBUTE

# Access a class attribute?
INSTANCE.ATTRIBUTE
CLASS.ATTRIBUTE

# Modify a class attribute?
CLASS.ATTRIBUTE = VALUE      # modifying an instance defines a new instance attribute, does not affect the actual class attribute

```

<hr> 

### `__init__()` Function
- The `__init__()` function is called automatically every time a class is used to create a new object. 
  - It is used to assign values to object properties or perform other set-up operations.

```Python
class CLASS:
  def __init__(self, PROP1, PROP2, ...):
    self.PROP1 = VAL1
    self.PROP2 = VAL2
    .
    .
    .

```

<hr> 

### `__str__()` Function
- The `__str__()` function controls what should be returned when the class object is represented as a string (printed).
  - Often used in combination with format strings. 

```Python
class CLASS:
  ...    # __init__() stuff
  def __str__(self):
    return STRING_REPRESENTATION_OF_CLASS    # often a format string
  
```

<hr>

### Iterators
- Iterators are objects that contain a countable number of values.

> Strings, lists, tuples, dictionaries, and sets are iterable objects, but not iterators.
```Python
# Get an iterator from an iterable object?
ITERATOR = iter(ITERABLE)

# Define an iterator class?
class ITERATOR:
  def __iter__(self, ...):
    ITER_CODE    # can initialize, like __init__()
    return self  # required
  def __next__(self):
    NEXT_CODE
    return NEXT_ELEMENT

# Add a terminating condition to __next__() in an iterator class?
def __next__(self):
  if CONDITION:
    NEXT_CODE
    return NEXT_ELEMENT
  else:
    raise StopIteration

```
<hr>

### Inheritance
- Inheritance allows a child class to inherit the methods and properties of a parent class, with the possibility of overriding. 
  - A method/property defined in a child class will override a method/property of the same name in the parent class. 

```Python
# Create a child class?
class CHILD_CLASS(PARENT_CLASS):
  PASS

# Inherit a parent class' __init__() function?
class CHILD(PARENT):
  def __init__(self, ...):
    super().__init__(self, ...)
    ...              # remember to update parameters if properties are added 
class CHILD(PARENT):
  def __init__(self, ...):
    PARENT.__init__(self, ...)
    ...              # remember to update parameters if properties are added 

# Call an overridden parent class method?
super().METHOD()

```

<hr>

### Polymorphism
- **Function Polymorphism**: when a function can be used on different objects/classes
- **Class Polymorphism**: when multiple classes have a method with the same name
- **Inheritance Class Polymorphism**: when child classes have a method (overwritten or not) with the same name as its parent class

<hr>

### Modules
- Modules are files containing sets of functions you want to include in an application (like libraries).
- Local modules with the same name as built-in modules have priority. 

```Python
# Create a module?
"Save the code in a file ending with .py"

# Use a module?
import MODULE

# Create an alias for a module on import?
import MODULE as ALIAS        # ALIAS can be used for dot operations instead of MODULE

# Import a specific function/variable from a module?
from MODULE import FUNCTION_OR_VARIABLE    # you can access FUNCTION_OR_VARIABLE directly, without using a dot operator on MODULE

# List all the functions/variables in a module?
LIST_OF_FUNCTIONS_AND_VARIABLES = dir(MODULE)

# Use a function from a module?
MODULE.FUNCTION()

# Access a variable from a module?
MODULE.VARIABLE

```

<hr>

### `datetime` Module
- [`strftime()` Format Codes](https://www.w3schools.com/python/python_datetime.asp)

```Python
import datetime

# Get the current time?
CURRENT_TIME = datetime.datetime.now()      # Default Format: YYYY-DD-MM HH:mm:ss.ms

# Get the current year?
YEAR = datetime.datetime.now().year      # first datetime is the module
                                         # second datetime is a class in the datetime module

# Create a date object?
DATE = datetime.datetime(YEAR, MONTH, DAY)

# Format a date object into a readable string?
DATE.strftime(FORMAT_CODE)      # check link above for legal format codes

```

<hr>

### `math` Module

```Python
import math

# Find the maximum/minimum value in an iterable?
MAXIMUM = max(ITERABLE)
MINIMUM = min(ITERABLE)

# Get the absolute (positive) value of a specific number?
ABS_VAL = abs(NUMBER)

# Raise a number to the power of another number?
pow(BASE, EXPONENT)
BASE ** EXPONENT

# Round a number up/down to the nearest integer?
ROUNDED_UP = math.ceil(NUMBER)
ROUNDED_DOWN = math.floor(NUMBER)

# Get the value of pi?
math.pi

```

<hr>

### `json` Module
```Python
import json

# Parse a JSON string?
PARSED = json.loads(JSON_STRING)      # result is a dictionary

# Convert a Python object to a JSON string?
JSON_STRING = json.dumps(OBJECT)      # all basic data types (except complex) + True/False/None can be converted into a JavaScript equivalent

# Convert a Python object to a JSON string AND format?
json.dumps(OBJECT, indent=INDENT_AMOUNT)      # controls indentation
json.dumps(OBJECT, separators=(OBJECT_SEPARATOR, KEY_VALUE_PAIR_SEPARATOR))     # controls separator characters
                                                                                # Default Values: OBJECT_SEPARATOR = ", ", KEY_VALUE_PAIR_SEPARATOR = ": "

# Convert a Python object to a JSON string AND sort the keys?
json.dumps(OBJECT, sort_keys=True)

```

<hr>

### Regular Expression (RegEx) Module
- Regular Expressions are sequences of characters that form a search pattern.
  - You can use RegEx to check if a string contains a search pattern.
 
> [RegExOne Tutorial Exercises](https://regexone.com/lesson/introduction_abcs) <br>
> [RegEx Crossword](https://regexcrossword.com)

```Python
import re

# Search a string for the FIRST substring that matches a RegEx?
MATCH_OBJECT = re.search(REGEX, STRING)    # returns a Match Object or None (if no matches are found)

# Get the (start, end) indices of a matched substring from a Match Object?
INDICES = MATCH_OBJECT.span()    # returns a tuple

# Retrieve the original string that was searched from a Match Object?
STRING = MATCH_OBJECT.string

# Get all of the capture groups from a Match Object?
CAPTURE_GROUPS = MATCH_OBJECT.group()      # returns a tuple

# Get the n-th capture group from a Match Object?
CAPTURE_GROUP = MATCH_OBJECT.group(N)      # indexing starts at 1, 0 is the full match

# Get a named capture group from a Match Object?
CAPTURE_GROUP = MATCH_OBJECT.group(NAME)  

# Search a string for ALL substrings that matche a RegEx?
LIST_OF_MATCHES = re.findall(REGEX, STRING)      # returns a list of substrings

# Split a string at each match of a RegEx?
LIST_OF_SUBSTRINGS = re.split(REGEX, STRING)

# Construct a new string that replaces N substrings that match a RegEx in some original string with some other string?
NEW_STRING = re.sub(REGEX, OTHER_STRING, STRING, N)    # Default Value: N = 1

```

<hr> 

### Flags
- Flags are additional parameters that can be added to RegEx functions.
  - Example Syntax: `re.findall(REGEX, STRING, FLAG)`

```Python
# Only count matches that contain ASCII characters only?
re.A
re.ASCII

# Count matches where . can be the newline character (usually excepted)?
re.S
re.DOTALL

# Only count matches found at the beginning of a line?
re.M
re.MULTILINE

# Count matches, but ignore whitespace and comments in the RegEx?
re.X
re.VERBOSE
# Example RegEx: "hi # look for matches of hi" searches for "hi"

```

<hr>

### Metacharacters and Special Sequences
- Metacharacters are characters with special meanings for Regular Expressions.

```Python
\           # escape a special character or indicate a special sequence
.           # match any character, except newline
[]          # match any one character from the set, see more later

()          # capture groups for returning or later reference, indexing starts at 1
(?P<NAME>)  # capture a group and name it
(?:)        # group without capturing
\N          # backreference the n-th captured group in the RegEx

^()         # anchors match to the START of the string (or line with re.M)
()$         # manchors match to the END of the string (or line with re.M)

()*         # matches ZERO OR MORE instances of the preceding group or single char
()+         # matches ONE OR MORE instances of the preceding group or single char 
()?         # matches ZERO OR ONE instances of the preceding group or single char
(){N}       # matches N instances of the preceding group or single char
(){N,}      # matches N OR MORE instances of the preceding group or single char
(){N,M}     # matches BETWEEN N and M instances of the preceding group or single char
# note: if brackets are ommitted, then only the preceding character will be quantified

STRING1|STRING2    # match contains STRING1 or STRING2

```

<hr>

### Special Sequences
- Special sequences are escaped characters with special meanings for Regular Expressions. 

```Python
\d       # match any digit (0-9)
\D       # match any non-digit
\s       # match any whitespace character
\S       # match any non-whitespace character
\w       # match any word character (alphanumeric and _)
\W       # match any non-word character

\A()    # find the match at the START of a string
()\Z    # find the match at the END of a string
\b()    # find matches at the START of words
()\b    # find matches at the END of words
\b()\b  # find standalone matches (exclude matches that are part of bigger words)
\B()    # find matches NOT at the START of words
()\B    # find matches NOT at the END of words
\B()\B  # find embedded matches (exclude matches that are standalone words)

````

<hr>

### RegEx Sets
- RegEx sets contain characters from which any single character can be matched in a RegEx.

> Metacharacters have no special meaning in sets. 

```Python
[abc]      # match one of a, b, or c
[a-c]      # match a letter from a to c alphabetically
[^abc]     # match any character EXCEPT a, b, or c (negate set)

[0-9]      # match any digit
[a-z]      # match any lowercase letter
[a-zA-Z]   # match any letter

```

<hr>

### PIP
- PIP is a package manager for Python packages.
  - Packages contain all the files required for a module.
  - Find packages at [https://pypi.org](https://pypi.org).
 
```Python
# Use a package?
pip install PACKAGE      # terminal input, NOT code
import PACKAGE           # ensure PACKAGE is installed into the same directory as the Python script

# Remove a package?
pip uninstall PACKAGE    # terminal input, NOT code

# List all installed packages?
pip list                 # terminal input, NOT code

```

<hr>

### Python Virtual Environment
- A viritual environment is a separate container for a Python project with its own set of installed packages and Python interpreter.
  - This prevents conflicts, makes projects more portable, and keeys the system Python installation clean.
 
```bash
# Create a virtual environment?
python -m venv PROJECT_NAME      # terminal input, NOT code

# Activate a virtual environment?
PROJECT_NAME\Scripts\activate    # terminal input, NOT code

# Execute a Python script in the virtual environment?
python SCRIPT.py                 # terminal input in the venv, NOT code

# Deactivate a virtual environment?
deactivate                       # terminal input in the venv, NOT code

# DElete a virtual environment?
rmdir /s /q PROJECT_NAME         # terminal input, NOT code

```





















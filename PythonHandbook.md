# Python Handbook

## Table of Contents

> [Language Details](#language-details) 

> Variables <br>
>> [Variable Definition](#variable-definition) <br>
>> [Local Variables vs Global Variables](#local-variables-vs-global-variables) <br>

> Basic Structures <br>
>> [Commenting](#commenting) <br>
>> [Conditionals](#conditionals) <br>
>> [Match-Case](#match-case) <br>
>> [Loops](#loops) <br>

> Basic Data Types <br>
>> [Type Casting](#type-casting) <br>
>> [Numeric Data Types](#numeric-data-types) <br>
>> [Strings](#strings) <br>
>>> [Substring Functions](#substring-functions) <br>
>>> [Format Strings](#format-strings) <br>
>>
>> [Lists](#lists) <br>
>>> [List Sorting Functions](#list-sorting-functions) <br>
>>> [List Comprehension](#list-comprehension) <br>
>>> [Shallow Copy vs Deep Copy (of Nested Lists)](#shallow-copy-vs-deep-copy-of-nested-lists) <br>
>>> [Slicing](#slicing) <br>
>>
>> [Tuples](#tuples) <br>
>> [Dictionaries](#dictionaries) <br>
>> [Sets](#sets) <br>

> [Functions](#functions) <br>
>> [Docstrings](#docstrings) <br>
>> [Parameters vs Arguments](#parameters-vs-arguments) <br>
>> [Positional Arguments, Keyword Arguments, and Arbitrary Arguments](#positional-arguments-keyword-arguments-and-arbitrary-arguments) <br>
>> [Lambda Functions](#lambda-functions) <br>

> Object Oriented Programming
>> [Classes](#classes) <br>
>>> [`__init__()` Function](#init-function) <br>
>>> [`__str__()` Function](#str-function) <br>
>>> [Iterators](#iterators) <br>
>>
>> [Inheritance](#inheritance) <br>
>> [Polymorphism](#polymorphism) <br>

<hr>

### Language Details
- Python is an object oriented programming language. 
- Indentation defines scope.
- New lines terminate statements. 
- Files end in `.py`.

> - No pre-defined integer limit. 

<hr>

### Variable Definition
- Variables are **DYNAMICALLY TYPED** -> Variables take on the type of the values they refer to at runtime.

```Python
# Define a variable?
VARIABLE_NAME = EXPRESSION

# Define multiple variables at once?
VAR1, VAR2, ... = EXP1, EXP2, ...

# Swap the values of two variables?
VAR1, VAR2 = VAR2, VAR1

# Print multiple variables?
print(VAR1, VAR2, ...)

```

<hr>

### Local Variables vs Global Variables
- **Local Variables**: defined inside a function -> only accessible within the function (local scope)
- **Global Variables**: defined outside a function -> accessible throughout the code (global scope)

> - Variables are only available from inside the region they are created. 
> - In a function, local variables with the same name as global variables have priority.
> - Parameters are local variables.
> - Declaring a local variable as global will cause an error.
```Python
# Define a global variable in a function (local scope)?
# Allow a global variable to be MODIFIED in a function (local scope)?
global GLOBAL_VARIABLE_NAME    # will throw an error if GLOBAL_VARIABLE NAME is the name of a local variable
                               # global variables are accessible (without modifications) without declaration

# Define a variable to belong to the outer function of a nested function?
def FUNCTION1():
  ...
  def FUNCTION2():
    nonlocal VARIABLE    # belongs to FUNCTION1
    ...

```

<hr>

### Commenting
```Python
# single-line comment

"""
multi-line
comment

works because unassigned string literals have no effect
"""

```

<hr>

### Conditionals
```Python
# General Syntax
if CONDITION1:
  IF_CODE
elif CONDITION2:
  ELIF1_CODE
.
.
.
else:
  ELSE_CODE

# Ternary Operator
IF_CODE if CONDITION else ELSE_CODE

# Shorthand If
if CONDITION: CODE

```
<hr>

### Match-Case
```Python
# General Syntax
match EXPRESSION:
  case VALUE1:
    CASE1_CODE
  case VALUE2:
    CASE2_CODE
  .
  .
  .
  case _:        # default case
    DEFAULT_CODE

# Combine multiple values for a case?
case VALUE1 | VALUE2 | ...:
  CASE_CODE

# Add an extra condition check to a case?
case VALUE if CONDITION:
  CASE_CODE

```

<hr>

### Loops
```Python
# For Loop - Standard Case
for COUNTER in range(COUNT):
  LOOP_CODE

# For Loop - General Case
for COUNTER in range(START, END, STEP):        # END is excluded
  LOOP_CODE

# For Loop - Iterable Object Case
for ELEMENT in ITERABLE:
  LOOP_CODE

# While Loop
while CONDITION:
  LOOP_CODE

# Force a loop to terminate?
break

# Skip an iteration of a loop?
continue

```

<hr>

### Type Casting
- Each basic data type has a corresponding constructor function that can be used to explicitly convert or create values of that type.

> - Casting from float to integers risks data loss by truncation.
> - You cannot cast from complex to int or float. 

```Python
# Get the data type of a value?
type(VALUE)

```
<hr>

### Numeric Data Types
1. `int`
2. `float`
3. `complex`

```Python
# Define a scientific number?
SCIENTIFIC_NUMBER = DECIMAL e POWER_OF_TEN
avagadros_number = 6.022e23    # example

# Define a complex number?
COMPLEX_NUMBER = REAL_PART + IMAGINARY_PARTj
c = 2 + 2 j    # example

```
<hr>

### Strings
- Python has no "character" data type, so strings are lists of length 1 substrings.

```Python
# Define a string?
STRING = '...'
STRING = "..."   # can use double or single quotes

# Define a multi-line string?
STRING = """ .
.
. """
STRING = '''.
.
. '''            # can use three double or three single quotes

# Get the length of a string?
LENGTH = len(STRING)

# Loop through the characters of a string?
for CHARACTER in STRING:
    LOOP_CODE

# Construct a new string that is the combination of multiple strings?
NEW_STRING = STRING1 + STRING2 + ...

# Remove whitespace from the end and the beginning of a string?
STRING.strip()

# Convert a string to uppercase/lowercase?
STRING.upper()
STRING.lower()

# Check if a string is entirely whitespace?
STRING.isspace()

# Check if a string is entirely alphanumeric?
STRING.isalnum()
# note: there are many similar functions

```

<hr>

### Substring Functions
```Python
# Check if a specific substring is in a string?
SUBSTRING in STRING

# Check if a string ends with a specific substring?
STRING.endswith(SUBSTRING)

# Find the index of the FIRST instance of a specific substring in a string?
STRING.find(SUBSTRING)

# Find the index of the LAST instance of a specific substring in a string?
STRING.rfind(SUBSTRING)

# Count the instances of a specific substring in a string?
COUNT = STRING.count(SUBSTRING)

# Split a string into a list of substrings with respect to some separator character?
SUBSTRING_LIST = STRING.split(SEPARATOR)

# Insert some other string at a specific index of a string?
STRING = STRING[:INDEX] + OTHER_STRING + STRING[INDEX+1:]        # slicing, see more later

# Replace a substring of a string with another string?
STRING = STRING[:SUBSTRING_START] + OTHER_STRING + STRING[SUBSTRING_END:]            # slicing, see more later

# Replace all instances of a spsecific substring in a string with another string?
STRING.replace(REPLACED_STRING, REPLACING_STRING)



```

<hr>

### Format Strings
- Format strings are strings that contain some variable or expression.

```Python
# Define a format string?
FSTRING = f"...{VARIABLE_OR_EXPRESSION}..."

# Define a format string where a numeric value is formatted to two decimal places?
FSTRING = f"...{NUMERIC_VALUE.2f}..."

```

<hr>

### Lists
**General Properties**:
- Ordered
- Changeable
- Allows Duplicate Elements

> Lists can contain any data type (even different data types).

```Python
# Define a list?
LIST = [ELEMENT1, ELEMENT2, ...]

# Access the n-th element of a list (Indexing)?
LIST[N]        # indexing starts at 0

# Get the length of a list?
LENGTH = len(LIST)

# Loop through the elements of a list?
for ELEMENT in LIST:
  LOOP_CODE

# Loop through the elements of a list by indices?
for INDEX in range(len(LIST)):
  LOOP_CODE

# Check if a specific element is in a list?
ELEMENT in LIST

# Add a specific element to the END of a list?
LIST.append(ELEMENT)

# Insert a specific element at a specific index in a list?
LIST.insert(INDEX, ELEMENT)

# Remove the FIRST instance of a specific element from a list?
LIST.remove(ELEMENT)

# Remove the LAST element of a list?
LIST.pop()

# Remove the element at a specific index from a list?
LIST.pop(INDEX)

# Remove every element in a list?
LIST.clear()

# Reverse a list?
LIST.reverse()

# Construct a new list that is the reverse of a list?
NEW_LIST = LIST[::-1]    # slicing, see more later

# Replace a sublist of a list with another list?
LIST[SUBLIST_START:SUBLIST_END] = OTHER_LIST    # slicing, see more later
                                                # note: the length of LIST will change if len(OTHER_LIST) != len(SUBLIST)

# Construct a new list that is the combination of multiple lists?
NEW_LIST = LIST1 + LIST2 + ...

# Merge multiple lists into a single list?
LIST.extend(LIST1, LIST2, ...)      # works with any iterable

```
<hr>

### List Sorting Functions
```Python
# Sort a list alphumerically, increasing?
LIST.sort()

# Sort a list alphanumerically, decreasing?
LIST.sort(reverse = True)

# Sort a list alphanumerically, case-insensitive, increasing?
LIST.sort(key = str.lower)

# Sort a list using a custom function?
LIST.sort(key = CUSTOM_FUNCTION)        # CUSTOM_FUNCTION should return some number, which will be used to sort by increasing return value

```

<hr>

### List Comprehension
- Shorthand syntax for constructing new lists using the elements of an existing list.
```Python
NEW_LIST = EXPRESSION for ELEMENT in LIST if CONDITION      # note: EXPRESSION is often the same as ELEMENT
                                                            # example: ELEMENT for ELEMENT in LIST if x > 0

```

<hr>

### Shallow Copy vs Deep Copy (of Nested Lists)
- **Shallow Copy**: a copy where inner objects share addresses with the original, but the outer list object is diferent
  - Changes made to MUTABLE inner objects (other lists) are reflected in the copy AND the original.
- **Deep Copy**: a copy where no addresses are shared
  - Changes made to MUTABLE inner objects (other lists) are only reflected in the object that was changed. 

```Python
# Make a shallow copy of a nested list?
COPY = ORIGINAL[:]    # slicing, see more later
COPY = ORIGINAL.copy()

# Make a deep copy of a nested list?
"1. Directly copy immutable inner objects."
"2. Recursively make copies of mutable inner objects."

```

<hr>

### Slicing
- Shorthand syntax for accessing sublists of lists (and substrings of strings) by using a range of indices. 
  - You can slice from the end of a list by using negative indices. -1 is the last index. 

> Strings are IMMUTABLE, so standard slice reassignment is not permitted.

```Python
LIST[START:END:STEP]      # END is excluded and :STEP is optional
                          # Default Values: START = 0, END = len(LIST), STEP = 1

# Slice to the end?
LIST[START:]    # omit END

# Slice from the start?
LIST[:END]      # omit START

# Slice from the end?
LIST[END:START]    # where END and START use negative indices

# Replace a sublist of a list with another list? (Slice Reassignment)
LIST[START:END] = OTHER_LIST      # does NOT work on strings because strings are immutable

# Replace a substring of a string with another string?
STRING = STRING[:SUBSTRING_START] + OTHER_STRING + STRING[SUBSTRING_END:]

```

<hr>

### Tuples
**General Properties**:
- Ordered
- Unchangeable
- Allows Duplicate Elements

> Tuples can contain any data type (even different data types).
> Tuples are immutable lists. 

```Python
# Define a tuple?
TUPLE = (ELEMENT1, ELEMENT2, ...)

# Construct a tuple with one element?
TUPLE = (ELEMENT,)

# Unpack a tuple into variables?
(VAR1, VAR2, ...) = TUPLE      # if * is added in front of a variable, then that variable will be filled with values from
                               # the tuple until the number of values left equals the number of variables left

# Find the index of a specific element of a tuple?
TUPLE.index(ELEMENT)

# Count the instances of a specific element in a tuple?
TUPLE.count(ELEMENT)

# Construct a new tuple that is the combination of multiple tuples?
NEW_TUPLE = TUPLE1 + TUPLE2 + ...

# Modify a value in a tuple?
TUPLE_AS_LIST = list(TUPLE)    # convert to a mutable list
# change TUPLE_AS_LIST
TUPLE = tuple(TUPLE_AS_LIST)   # convert back to a immutable tuple

```

<hr>

### Dictionaries
**General Properties**:
- Ordered
- Changeable
- Does NOT Allow Duplicate KEYS (Duplicate VALUES Allowed)

> Keys are like indices. 

```Python
# Define a dictionary?
DICT = {KEY1:VAL1, KEY2:VAL2, ...}        # keys must be unique

# Access the value associate with a specific key in a dictionary?
DICT[KEY]
DICT.get(KEY)

# Access the value associated with a specific key in a NESTED dictionary?
DICT[OUTER_KEY][INNER KEY]

# Add a key:value pair to a dictionary?
DICT[KEY] = VALUE

# Remove an element associated with a specific key in a dictionary?
DICT.pop(KEY)

# Remove the LAST element in a dictionary?
DICT.popitem()

# Construct a list of keys of a dictionary?
KEYS = DICT.keys()      # KEYS will change if DICT changes

# Construct a list of values of a dictionary?
VALUES = DICT.values()  # VALUES will change if DICT changes

# Construct a list of key:value pairs of a dictionary?
KVPS = DICT.items()     # KVPS will change if DICT changes
                        # key:value pairs are stored as TUPLES in a list

# Loop through the keys AND the values of a dictionary?
for key, value in DICT.items():
  LOOP_CODE

# Check if a specific key is in a dictionary?
KEY in DICT

# Check if a specific value is in a dictionary?
VAL in DICT.values()

# Merge multiple dictionaries into one dictionary?
DICT.update(DICT1, DICT2, ...)      # works with any iterable of key:value pairs

```

<hr>

### Sets
**General Properties**:
- Unordered (No Indexing)
- Unchangeable (set elements must be immutable, but you can add and remove elements to the set)
- Does NOT Allow Duplicate Elements

> Sets can contain any data type (even different data types).
> True and 1 considered duplicates.
> False and 0 are considered duplicates.

```Python
# Define a set?
SET = {ELEMENT1, ELEMENT2, ...}

# Loop through each element of a set?
for ELEMENT in SEt:
    LOOP_CODE

# Add an element to a set?
SET.add(ELEMENT)

# Remove a random element from the set?
SET.pop()    # returns the removed item

# Remove a specific element from the set?
SET.remove(ELEMENT)      # raises an error if not found
SET.discard(ELEMENT)     # does NOT raise an error if not found

# Check if some set is the a subset of a set?
OTHER_SET.issubset(SET)

# Check if two sets are disjoint?
SET.isdisjoint(OTHER_SET)

# Construct a new set that is the UNION of multiple sets?
NEW_SET = SET1 | SET2 | ...        # only works with sets
NEW_SET = SET1.union(SET2, ...)    # works with any iterable

# Modify a set to be the UNION of the set with (multiple) other sets?
SET.update(SET1, SET2, ...)   # works with any iterables
SET |= OTHER_SET              # only works with one other set

# Construct a new set that is the INTERSECTION of multiple sets?
NEW_SET = SET1 & SET2 & ...               # only works with sets
NEW_SET = SET1.intersection(SET2, ...)    # works with any iterable

# Modify a set to be the INTERSECTION of the set with (multiple) other sets?
SET.intersection_update(SET1, SET2, ...)   # works with any iterables
SET &= OTHER_SET                           # only works with one other set

# Construct a new set that is the DIFFERENCE of multiple sets?
NEW_SET = SET1 - SET2 - ...               # only works with sets
NEW_SET = SET1.difference(SET2, ...)      # works with any iterable

# Modify a set to be the DIFFERENCE of the set with (multiple) other sets?
SET.difference_update(SET1, SET2, ...)   # works with any iterables
SET -= OTHER_SET                         # only works with one other set

# Construct a new set that is the SYMMETRIC DIFFERENCE of multiple sets?
NEW_SET = SET1 ^ SET2 ^ ...               # only works with sets
NEW_SET = SET1.difference(SET2, ...)      # works with any iterable

# Modify a set to be the SYMMETRIC DIFFERENCE of the set with (multiple) other sets?
SET.symmetric_difference_update(SET1, SET2, ...)   # works with any iterables
SET ^= OTHER_SET                                   # only works with one other set

```

<hr>

### Functions

```Python
# Define a function?
def FUNCTION(PARAM1, PARAM2, ...):
  FUNCTION_CODE
  return RETURN_VALUE        # optional

# Call a function?
FUNCTION(ARG1, ARG2, ...)

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

### Classes
- Classes are object constructors.
- Classes can have properties (variables) and methods (functions). 
- The `self` parameter of a object method is a reference to the current instance (object) of a class.
  - Used to access variables that belong to the class / object.
  - Can be named anything, but has to be the first parameter of any object method. 

```Python
# Define a class?
class CLASS:
  def __init__(self, PROPERTY, ...):
    INIT_CODE

  PROPERTY = VALUE

  . 
  .
  .

  def METHOD(self):
    METHOD_CODE

  .
  .
  .

# Define a class with no content?
class CLASS:
  pass

# Create an object of a class?
OBJECT = CLASS()

# Delete an object of a class?
del OBJECT

# Modify a property of an object?
OBJECT.PROPERTY = VALUE

# Delete a property of an object?
del OBJECT.PROPERTY

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

```

<hr>

### Polymorphism
- **Function Polymorphism**: when a function can be used on different objects/classes
- **Class Polymorphism**: when multiple classes have a method with the same name
- **Inheritance Class Polymorphism**: when child classes have a method (overwritten or not) with the same name as its parent class

<hr>

### Modules
- Modules are files containing sets of functions you want to include in an application (like libraries).

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
                                                                                # Default Values: (", ", ": ")

# Convert a Python object to a JSON string AND sort the keys?
json.dumps(OBJECT, sort_keys=True)

```



















# Python Handbook

## Table of Contents

> [Language Details](#language-details) <br>
> [Commenting](#commenting) <br>

> [Variables](#variables) <br>
>> [Local Variables vs Global Variables](#local-variables-vs-global-variables) <br>

> Control Flow <br>
>> [Conditionals](#conditionals) <br>
>> [Match-Case](#match-case) <br>
>> [Loops](#loops) <br>
>> [Try-Except](#try-except) <br>

> Primitive Data Types <br>
>> [Type Casting](#type-casting) <br>
>> [Numeric Data Types](#numeric-data-types) <br>
>> [Strings](#strings) <br>
>>> [Substring Functions](#substring-functions) <br>
>>> [Format Strings](#format-strings) <br>
>>

> Collections <br>
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
>> [User Input](#user-input) <br>

> Object Oriented Programming
>> [Classes](#classes) <br>
>>> [`__init__()` Function](#init-function) <br>
>>> [`__str__()` Function](#str-function) <br>
>>> [Iterators](#iterators) <br>
>>
>> [Inheritance](#inheritance) <br>
>> [Polymorphism](#polymorphism) <br>

> [Modules](#modules) <br>
>> [`datetime` Module](#datetime-module) <br>
>> [`math` Module](#math-module) <br>
>> [`json` Module](#json-module) <br>
>> [Regular Expression (RegEx) Module](#regular-expression-regex-module) <br>
>>> [Flags](#flags) <br>
>>> [Metacharacters](#metacharacters) <br>
>>> [Special Sequences](#special-sequences) <br>
>>> [RegEx Sets](#regex-sets) <br>
>> [PIP](#pip) <br>
>> [Python Virtual Environment](#python-virtual-environment) <br>

<hr>

### Language Details
- Indentation defines scope.
- New lines indicate the end of a statement.
- Scripts end in `.py`.

<hr>

### Variables
- Variables are **dynamically typed**.
  - A variable will take on the type of the value it refers to at runtime. 

```Python
# Define a variable?
VARIABLE_NAME = EXPRESSION

# Define multiple variables?
VAR1, VAR2, ... = EXP1, EXP2, ...

# Swap the values of two variables?
VAR1, VAR2 = VAR2, VAR1

# Print multiple variables?
print(VAR1, VAR2, ...)      # will be separated by a space

```

<hr>

### Commenting
```Python
# single-line comment

"""
multi-line
comment
"""

```

<hr>

### Local Variables vs Global Variables
- **Local Variables** => defined inside of a function => only accessible within the same function (local scope)
- **Global Variables** => defined in the main body => accessible throughout the main body (global scope)

<br>

- For functions: 
  - Parameters are local variables.
  - A local var with the same name as a global var will have priority.
  - Declaring a local var as global will raise an error.

```Python
# Define a global variable in a function?
global GLOBAL_VAR

# Allow a global var to be MODIFIED in a function?
global GLOBAL_VAR      # accessible without declaration (modification disallowed)

# Define a variable to belong to the outer function of a nested function?
def OUTER_FUNCTION():
  ...
  def 

# For a nested function, define a variable in the inner function to belong to the outer function?
def OUTER_FUNCTION():
  ...
  def INNER_FUNCTION():
    nonlocal VARIABLE     # belongs to OUTER_FUNCTION
    ...

```

<hr>

### Conditionals
```Python
# General Syntax
if IF_CONDITION:
  IF_CODE
elif ELIF1_CONDITION:
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

# Give a case multiple values?
case VALUE1 | VALUE2 | ...:
  CASE_CODE

# Give a case an extra condition check?
case VALUE if CONDITION:
  CASE_CODE

```

<hr>

### Loops
```Python
# For Loop - Standard Case
for COUNTER in range(COUNT):                   # loops from 0 to COUNT - 1
  LOOP_CODE

# For Loop - General Case
for COUNTER in range(START, END, STEP):        # loops from START to END - 1 by increments of STEP
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

### Try-Except
- Used to sanitize inputs. 
- [List of Built-In Python Exceptions](https://www.w3schools.com/python/python_ref_exceptions.asp)

```Python
# General Syntax
try:
  TRY_CODE                   # potentially raises an exception
except:
  EXCEPT_CODE                # handles any exceptions
else:
  ELSE_CODE                  # executes when no exceptions have been raised
finally:
  FINALLY_CODE               # always executes, regardless of any exceptions or lack thereof

# Handle a specific type of exception?
except EXCEPTION_TYPE:
  EXCEPT_CODE

# Raise an exception?
raise EXCEPTION_TYPE("PRINTED_EXCEPTION_STATEMENT")

```

<hr>

### Type Casting
- Data types have constructor functions that can be used to explictly convert (cast) or create values of that type.
- Casting from `float` to `int` risks data loss to truncation.
- You cannot cast from `complex` to `float` or `int`.

```Python
# Cast a specific value to string?
STRING = str(VALUE)

# Get the data type of a specific value?
type(VALUE)

```

<hr>

### Numeric Data Types
- Python has three numeric data types:
  - `int`
  - `float`
  - `complex`

<br>

- There is no pre-defined integer limit.
```Python
# Define a complex number?
COMPLEX_NUMBER = REAL_PART + IMAGINARY_PARTj
c = 2 + 2 j                    # example

# Define a scientific number?
SCIENTIFIC_NUMBER = DECIMAL e POWER_OF_TEN
avagadros_number = 6.022e23    # example

```

<hr>

### Strings
- Python has no "character" data type => strings are lists of length 1 substrings

```Python
# Define a string?
STRING = 'this is a string'
STRING = "this is a string"   # can use double or single quotes

# Define a multi-line string?
STRING = """ this
is a
string """
STRING = ''' this
is a
string '''            # can use three double or three single quotes

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
- Format strings are strings that can contain some placeholder expression.
  - Placeholders can also have modifers to specify their format. 

```Python
# Define a format string?
FSTRING = f"...{EXPRESSION}..."

# Choose a placeholder expression conditionally?
FSTRING = f"...{IF_EXPRESSION if CONDITION else ELSE_EXPRESSION}..."

# Modify a placeholder expression to have n decimal points?
FSTRING = f"...{EXPRESSION:.Nf}..."
FSTRING = f"...{EXPRESSION:.2f}..."    # example: two decimal points

# Modify a placeholder expression to use a comma as a thousand separator?
FSTRING = f"...{EXPRESSION:,}..."

# Modify a placeholder expression to be in scientific format?
FSTRING = f"...{EXPRESSION:e}..."
FSTRING = f"...{EXPRESSION:E}..."

# Modify a placeholder expression to be a percentage?
FSTRING = f"...{EXPRESSION:%}..."

# Modify a placeholder expression to left/right/center align within specified available space?
FSTRING = f"...{EXPRESION:<SPACE}..."      # left align within SPACE characters
FSTRING = f"...{EXPRESION:>SPACE}..."      # right align within SPACE characters
FSTRING = f"...{EXPRESION:^SPACE}..."      # center align within SPACE characters

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

### User Input
- It is good practice to validate any user input using try-except to check if the user provides valid input.

```Python
# Get user input from keyboard?
INPUT = input(PROMPT_STRING)     # Python stops executing and waits for input before continuing
                                 # PROMPT_STRING is optional
                                 # INPUT is a string

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





















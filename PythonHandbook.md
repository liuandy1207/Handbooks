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
>>> [List Comprehension](#list-comprehension) <br>
>>> [Shallow Copy vs Deep Copy (of Nested Lists)](#shallow-copy-vs-deep-copy-of-nested-lists) <br>
>>> [Slicing](#slicing) <br>
>>
>> [Tuples](#tuples) <br>
>> [Dictionaries](#dictionaries) <br>
>> [Sets](#sets) <br>
>> [Functions](#functions) <br>

<hr>

### Language Details
- Indentation defines scope.
- New lines terminate statements. 
- Files end in `.py`.

> No pre-defined integer limit. 

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
- Local -> defined inside a function -> accessible only within the function
- Global -> defined outside a function -> accessible throughout the code

> - In a function, local variables with the same name as global variables have priority.
> - Parameters are local variables.
> - Declaring a local variable as global will cause an error.
```Python
# Allow a global variable to be MODIFIED in a function>
global GLOBAL_VARIABLE_NAME    # will throw an error if GLOBAL_VARIABLE NAME is the name of a local variable
                               # global variables are accessible (without modifications) without declaration

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
'STRING'
"STRING"    # can use double or single quotes

# Multi-Line Strings
"""
MULTI-LINE
STRING
"""
'''
MULTI-LINE
STRING
'''        # can use three double or three single quotes

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

# Insert another string between specifed indices of a string?
STRING = STRING[:START] + OTHER_STRING + STRING[END:]        # slicing, see more later

# Replace all instances of a spsecific substring in a string with another string?
STRING.replace(REPLACED_STRING, REPLACING_STRING)

```

<hr>
??????
### Format Strings
Format strings leave space for variables/expressions to be inserted in them. <br>

```Python
f"... {<VARIABLE OR EXPRESSION>} ..."

## Format the variable/expression to have two decimal places?
f"... {<VARIABLE>.2f} ..."

```

<hr>

### Lists
Properties:
1. Ordered
2. Changeable
3. Allows duplicate values
4. Can contain any data type (even different data types)

```Python
<LIST> = [<ELEMENT>, ...]

# Access the n-th element of a list?
<LIST>[<N>]   # indexing starts at 0

# Get the length of a list?
<LENGTH> = len(<LIST>)

# Loop through a list's elements?
for <ELEMENT> in <LIST>:
  <CODE>

# Loop through a list's indices?
for <INDEX> in range(len(<LIST>)):
  <CODE>

# Check if an specific element is in a list?
<ELEMENT> in <LIST>

# Add a specific element to the end of a list?
<LIST>.append(<ELEMENT>)

# Insert an element at a specified index in a list?
<LIST>.insert(<INDEX>, <ELEMENT>)

# Remove the LAST element of a list?
<LIST>.pop()

# Remove the element at a specified index from a list?
<LIST>.pop(<INDEX>)

# Remove the FIRST instance of a specified element from a list?
<LIST>.remove(<ELEMENT>)

# Clear a list?
<LIST>.clear()

# Reverse a list?
<LIST>.reverse()

# Construct a new list that is the reverse of another list?
<NEW LIST> = <LIST>[::-1] # slicing

# Sort a list?
<LIST>.sort()   # alphanumeric, increasing
<LIST>.sort(reverse = True) # alphanumeric, decreasing
<LIST>.sort(key = str.lower)  # case-insensitive
<LIST>.sort(key = <CUSTOM FUNCTION>) # <FUNCTION> should return some number, list will be ordered by increasing return value

# Replace a sublist with another list?
<LIST>[<REPLACE START>:<REPLACE END>] = <REPLACING LIST>    # slicing
# note: <LIST> length will change if items inserted does not match items replaced

# Merge multiple lists into a single list?
<LIST1>.extend(<LIST2>, ...)    # works with any iterable

# Combine multiple lists into a new list?
<NEW LIST> = <LIST1> + <LIST2> + ...

```

<hr>

### List Comprehension
Create a new list using the elements of an existing list.
```Python
<NEW LIST> = [<EXPRESSION> for <ELEMENT> in <LIST> if <CONDITION>]
# <EXPRESSION> is often the same as <ELEMENT> -> x for x in <LIST>

```
<hr>

### Shallow Copy vs Deep Copy (of Nested Lists)
- Shallow Copy: a copy where inner objects share addresses with the original (outer list object is different)
- - Changes made to MUTABLE INNER OBJECTS (other lists) will affect the copy AND the original. 
- Deep Copy: a copy where no addresses are shared <br>
- - Changes made to MUTABLE INNER OBJECTS (other lists) will only affect the object that was changed. 

```Python
# Make a shallow copy of a nested list?
<COPIED LIST> = <ORIGINAL LIST>[:]  # slicing
<COPIED LIST> = <ORIGINAL LIST>.copy()

# Make a deep copy of a nested list?
"Recursively make copies of mutable inner objects."
"Immutable inner objects are copied directly."

```

<hr>

### Slicing
Access a subset of a string or a list. <br>

> STRINGS are IMMUTABLE, so slice reassignment is not permitted.
> You can slice from the end to the start with negative indexing. -1 is the last index. 

```Python
<LIST>[<START>:<END>:<STEP>]
# <END> is excluded, <STEP> is optional
# Default <START> = 0, <END> = len(<LIST>), <STEP> = 1

# Slice to the end?
<LIST>[<START>:]   # omit <END>

# Slice from the start?
<LIST>[:<END>]    # omit <START>

# Slice Reassignment
<LIST>[<SLICE>] = <CHANGE IN LIST>     # this does NOT work on strings because strings are immutable
<STRING> = <STRING>[:<SLICE START>] + <CHANGE IN STRING> + <STRING>[<SLICE END>:]

```

<hr>

### Tuples
Properties:
1. Ordered
2. Unchangeable
3. Allows duplicate elements
4. Can contain any data type (even different data types)
   
> Tuples are immutable lists.

```Python
<TUPLE> = (<ELEMENT>, ...)

# Construct a tuple with one element?
<TUPLE> = (<ELEMENT>,)

# Unpack a tuple into variables?
(<VAR1>, <VAR2>, ...) = <TUPLE>
# note: if * is added in front of a variable, then that variable will be filled with values from the tuple into the number of values left matches the number of variables left

# Find the index of a specific value in a tuple?
<TUPLE>.index(<ELEMENT>)

# Count the instances of a specific value in a tuple?
<TUPLE>.count(<ELEMENT>)

# Combine multiple tuples into a new tuple? 
<NEW TUPLE> = <TUPLE1> + <TUPLE2> + ...

# Change a value in a tuple?
<LIST> = list(<TUPLE>)  # convert to a list
# change the list
<TUPLE> = tuple(<LIST>)  # convert back to a tuple

```

<hr>


### Dictionaries
Properties:
1. Ordered
2. Changeable
3. Does NOT Allow Duplicate KEYS

> Keys are like named indices. 

```Python
<DICTIONARY> = {<KEY>:<VALUE>, ...}    # keys must be unique

# Access the value associated with a specific key in a dicitionary?
<DICT>[<KEY>]
<DICT>.get(<KEY>)

# Access the value associated with a specific key in a NESTED dictioanry?
<DICT>[<OUTER KEY>][<INNER KEY>]

# Add a key:value pair to a dictionary?
<DICT>[<KEY>] = <VALUE>

# Remove an element associated with a specific key?
<DICT>.pop(<KEY>)

# Remove the LAST element?
<DICT>.popitem()

# Construct a list of keys of a dictionary?
<KEYS> = <DICT>.keys()     # will change if <DICT> changes

# Construct a list of values of a dictionary?
<VALUES> = <DICT>.values()    # will change if <DICT> changes

# Construct a list of key:value pairs of a dictionary?
<KVP> = <DICT>.items()    # stored as TUPLES in a list, will change if <DICT> changes

# Loop through both the keys and the values of a dictionary?
for key, value in <DICT>.items():
  <CODE>

# Check if a specific key is in a dictionary?
<KEY> in <DICT>

# Check if a specific value is in a dictionary?
<VALUE> in <DICT>.values()

# Merge two dictionaries into one?
<DICT1>.update(<DICT2>)    # works with any iterable with key:value pairs

```

<hr>

### Sets
Properties:
- Unordered (no indices)
- Unchangeable (cannot change set items themselves, but you can add and remove items)
- Does NOT allow duplicate elements
- Can contain any data type (even different data types)

> True and 1 / False and 0 are considered DUPLICATES.

```Python
<SET> = {<ELEMENT>, ...}

## Add an element?
<SET>.add(<ELEMENT>)

# Loop through each element?
for <ELEMENT> in <SET>:    # order will be different every time
  <CODE>

# Remove a random element?
<SET>.pop()    # returns the removed item

# Remove a specific element?
<SET>.discard(<ELEMENT>)    # does NOT raise error if not found
<SET>.remove(<ELEMENT>)     # raises error if not found

# Check if one set is the subset of another set?
<SET1>.issubset(<SET2>)

# Check if two sets are disjoint?
<SET1>.isdisjoint(<SET2>)

# Construct a set that is the UNION of multiple sets?
<NEW SET> = <SET1> | <SET2> | ...        # only works with sets
<NEW SET> = <SET1>.union(<SET2>, ...)    # works with iterables
# note: duplicates are excluded

# Modify a set to be the UNION of the set with multiple sets?
<SET1> |= <SET2>   # repeat for multiple sets
<SET1>.update(<SET2>, ...)

# Construct a set that is the INTERSECTION of multiple sets?
<NEW SET> = <SET1> & <SET2> & ...        # only works with sets
<NEW SET> = <SET1>.intersection(<SET2>, ...)    # works with iterables

# Modify a set to be the INTERSECTION of the set with multiple sets?
<SET1> &= <SET2>   # repeat for multiple sets
<SET1>.intersection_update(<SET2>, ...)

# Construct a set that is the DIFFERENCE of multiple sets?
<NEW SET> = <SET1> - <SET2> - ...        # only works with sets
<NEW SET> = <SET1>.difference(<SET2>, ...)    # works with iterables

# Modify a set to be the DIFFERENCE of the set with multiple sets?
<SET1> -= <SET2>   # repeat for multiple sets
<SET1>.difference_update(<SET2>, ...)

# Construct a set that is the SYMMETRIC DIFFERENCE of multiple sets?
<NEW SET> = <SET1> ^ <SET2> ^ ...        # only works with sets
<NEW SET> = <SET1>.symmetric_difference(<SET2>, ...)    # works with iterables

# Modify a set to be the SYMMETRIC DIFFERENCE of the set with multiple sets?
<SET1> ^= <SET2>   # repeat for multiple sets
<SET1>.symmetric_difference_update(<SET2>, ...)  

```

<hr>

# Functions

```Python
# Define a function?
def func(param1, ...)

```















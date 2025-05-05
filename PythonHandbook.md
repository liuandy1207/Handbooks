# Python Handbook

## Table of Contents

>[Language Details](#language-details) <br>

> Variables <br>
>> [Variable Assignment](#variable-assignment) <br>
>> [Local Variables vs Global Variables](#local-variables-vs-global-variables) <br>

> Basic Structures <br>
>> [Commenting](#commenting) <br>
>> [Conditionals](#conditionals) <br>
>> [Match-Case](#match-case) <br>
>> [Loops](#loops) <br>

> Basic Data Types <br>
>> [Casting](#casting) <br>
>> [Numeric Data Types](#numeric-data-types) <br>
>> [Strings](#strings) <br>

<hr>

### Language Details
- Indentation indicates scope.
- New lines indicate EoL.
- No pre-defined integer limit.
<hr>

### Variable Assignment
Variables have no type associated with them. <br>
Variables are free to change what data type they hold. <br>

```Python
<VARIABLE> = <EXPRESSION>

# Multiple Assignment
<VAR1>, <VAR2>, ... = <EXP1>, <EXP2>, ...
```
<hr>

### Local Variables vs Global Variables
- Local → defined inside a function, only accessible within the function <br>
- Global → defined outside a function, accessible throughout the code <br>

> Local variables have priority over global variables in a function. <br>
> Local variables cannot be declared global (error). <br>
> Parameters are local variables.

```Python
# Change a global variable in a function?
global <GLOBAL VARIABLE>    # declare the variable as global IN THE FUNCTION before changing it
# note: will throw an error if there is a local variable of the same name
# note: access to global variables is permitted without declaration

# Print multiple variables?
print(<VAR1>, <VAR2>, ...)  # will be separated by a space
```
<hr>

### Commenting
```Python
# single-line comment

"""
multi-line
comment

note: works because python ignores string literals
"""

```
<hr>


### Conditionals
```Python
if <CONDITION>:
  <CODE>
elif <CONDITION>:
  <CODE>
.
.
.
else:
  <CODE>

# Ternary Operator
<CODE> if <CONDITION> else <CODE>

# Shorthand If
if <CONDITION>: <CODE>
```
<hr>

### Match-Case
```Python
match <EXPRESSION>:
  case <VALUE>:    # general case
    <CODE>
  .
  .
  .
  case _:      # default case
    <CODE>

# Combine multiple cases?
case <VAL1> | <VAL2> | ...:
  <CODE>

# Add an extra condition check to a case?
case <VALUE> if <CONDITION>:
  <CODE>
```
<hr>

### Loops
```Python
# For Loop - Default Case
for <COUNTER> in range(<COUNT>):
  <CODE>

# For Loop - General Case
for <COUNTER> in range(<START>, <END>, <STEP>):    # <END> excluded
  <CODE>

# For Loop - Iterable Object
for <ELEMENT> in <ITERABLE>:
  <CODE>

# While Loop
while <CONDITION>:
  <CODE>

# Force a loop to terminate?
break

# Skip an iteration of a loop?
continue

```

<hr>

### Casting
Constructor functions can be used to specify a data type (cast).

> Casting from float to integer risks data loss to truncation.
> Complex numbers cannot be cast to other numeric data types.

```Python
# Get the data type of a value?
type(<VALUE>)
```
<hr>

### Numeric Data Types
- `int`
- `float`
- `complex`

```Python
# Define a scientific number?
<FLOAT> = <DECIMAL>e<POWER OF TEN>
avagadro = 6.022e23

# Define a complex number?
<COMPLEX> = <REAL> + <IMAGINARY>j
c = 2 + 2j

```
<hr>

### Strings
There is no "character" data type, so strings are lists of substrings of length 1. <br>

> Quotes can be used inside a string only if they do not match the quotes surrounding a string. <br>

```Python
'string'
OR
"string"

# Multi-Line Strings
"""
multi-line
string
"""
OR
'''
multi-line
string
'''

# Get the length of a string?
<LENGTH> = len(<STRING>)

# Loop through the characters of a string?
for c in <STRING>:
  <CODE>

# Combine multiple strings?
<NEW STRING> = <STRING1> + <STRING2> + ...

# Remove whitespace from the end and beginning of a string?
<STRING>.strip()

# Make a string uppercase/lowercase?
<STRING>.upper()
<STRING>.lower()

# Check if a string is entirely whitespace?
<STRING>.isspace()

# Check if a string is entirely alphanumeric?
<STRING>isalnum()

"""
SUBSTRING FUNCTIONS
"""

# Check if a specific substring is in a string?
<SUBSTRING> in <STRING>

# Find the FIRST index of a specific substring in a string?
<STRING>.find(<SUBSTRING>)    # returns -1 if the substring is not found

# Find the LAST index of a specific substring in a string?
<STRING>.rfind(<SUBSTRING>)   # returns -1 if the substring is not found

# Count the number of times a specific substring occurs in a string
<COUNT> = <STRING>.count(<SUBSTRING>)

# Replace all instances of a specific substring with another string?
<STRING>.replace(<GETS REPLACED>, <REPLACED BY>)

# Check if a string ends with a specific substring?
<STRING>.endswith(<SUBSTRING>)

# Split a string into a list of substrings at a separator character?
<LIST OF SUBSTRINGS> = <STRING>.split(<SEPARATOR>)

```

<hr>

### Format Strings
Format strings have placeholders for a variable or expression. <br>

```Python
f"... {<VARIABLE OR EXPRESSION>} ..."

## Format the variable/expression to have two decimal places?
f"... {<VARIABLE>.2f} ..."

```




# Python Handbook
<hr>

## Table of Contents

[Language Details](#language-details) <br>
[Variables](#variables) <br>
[Basic Structures](#basic-structures) → Conditionals, Match/Case, Loops

<hr>

## Language Details
- Indentation indicates scope.
- New lines indicate EoL.
- No pre-defined integer limit.
```Python
# comment

"""
multi-line
comment
"""
```


## Variables
```Python
# GENERAL CASE
<VARIABLE> = <EXPRESSION>

# MULTIPLE ASSIGNMENT
<VAR1>, <VAR2>, ... = <EXP1>, <EXP2>, ...

# LOCAL vs GLOBAL
"""
local: defined inside a function, only accessible inside
global: defined outside a function, accessible throughout the code

- a variable cannot be global and local
- local variables have priority over global variables in a function
"""

# Change a global variable in a function?
def f():
  global <GLOBAL VARIABLE>    # declare the variable as global before changing it
  ...
# note: access is permitted without declaration

# Print multiple variables?
print(<VAR1>, <VAR2>, ...)  # will be separated by a space
```

## Basic Structures
```Python
# Conditionals
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

# Match/Case
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





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


<hr>

### Language Details
- Indentation indicates scope.
- New lines indicate EoL.
- No pre-defined integer limit.
<hr>

### Variable Assignment
```Python
# GENERAL CASE
<VARIABLE> = <EXPRESSION>

# MULTIPLE ASSIGNMENT
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
def f():
  global <GLOBAL VARIABLE>    # declare the variable as global before changing it
  ...
# note: access is permitted without declaration

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





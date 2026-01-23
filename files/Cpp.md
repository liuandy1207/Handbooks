# C++

## Table of Contents

> [General](#general)
>> [Basic Data Types](#basic-data-types) <br>
>> [Variables](#variables) <br>
>> [Control Structures](#control-structures) <br>
>
> [Functions](#functions)

<hr>

## General
C++ is an extension of C with more features (classes, objects, exceptions, etc.).

### Basic Data Types
 -   `int`: integer values
 -   `float`: single-precision floating-point values
 -   `double`: double-precision floating-point values
 -   `char`: single characters
 -   `bool`: boolean values

### Variables
Variables must be declared with a data type before they can be used: `int x;`

### Control Structures
```c++
if (CONDITION) {
  // code
} else {
  // code
}


while (CONDITION) {
  // code
}


for (INIT; CONDITION; UPDATE) {
  // code
}


switch (VARIABLE) {
  case VALUE1:
    // code
  break;
  case VALUE2:
    // code
  break;
  // more cases
  default:
    // code
}
```

## Functions
```
RETURN_TYPE FUNCTION_NAME(PARAM_TYPE_1 PARAM_1, ...) {
  // code
  return RETURN_VALUE;
}





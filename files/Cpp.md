# C++

<hr>

## Table of Contents

> [General](#general)
>
> > [Basic Data Types](#basic-data-types) <br>
> > [Variables](#variables) <br>
> > [Control Structures](#control-structures) <br>
>
> [Functions](#functions)
>
> > [`main` Function](#main-function) <br>
> > [Input/Output](#inputoutput) <br>
> > [Logical Operators](#logical-operators)

<hr>

## General

- C++ is an extension of C with more features (classes, objects, exceptions, etc.).
- C++ is procedural (like C) and object-oriented.
- Memory management can be manual (like C) or can rely on constructors/decontructors and smart pointers.

### Basic Data Types

- `int`: integer values
- `float`: single-precision floating-point values
- `double`: double-precision floating-point values
- `char`: single characters
- `bool`: boolean values

### Variables

- Variables must be declared with a data type before they can be used: `int x;`
- C++ is statically typed (type determined at compilation)

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

do {
  // code
} while (CONDITION);


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

goto LABEL;
// code between is skipped
LABEL:
  // code
```

## Functions

```c++
RETURN_TYPE FUNCTION_NAME(PARAM_TYPE_1 PARAM_1, ...) {
  // code
  return RETURN_VALUE;
}
```

### `main` Function

- All C++ programs need a `main()` function.

```c++
int main() {
  // code
}

```

### Input/Output

```c++
#include <iostream>   // standard library for IO

std::cout << "HELLO WORLD!";   // print statement

```

### Logical Operators

- `&&`: AND
- `||`: OR
- `!`: NOT

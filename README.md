# Orange Juice Language Specifications

This is NOT a strict specification (yet). Just write down some thoughts on how this language should be.

## Data Types

Basic: `int`, `long`, `bool`, `string`

Special: bigint, bigdec

Structure: list, set, map

When compile into C++, list may be implemented using vector, queue, or list, depending on how the list is used.
(This might be changed if the implementation is too difficult.)

Self-define types.

```
pair := int[2]
# or
pair := list<int>[2]
```

```
node :=
    x: int
    y: int
```

```
circle :=
    x: int
    y: int
    r: int
    area: ->
        return PI * r ^ 2
```

## Variables

OJ lang is static-typed. The compiler will always try to guess the data type if possible.

```
# One variable
int a
# Multiple variables of same type
int a, b
# List without fixed length
int a[]
# List with fixed length
int a[100]
# Same as above
a = list<int>(100)
```

Implicitly declare of variables. In the example below, the type of result is defined by the return value of `func`.

```
result = func()
```

`result` will take the data type from function `func`.

## Input & output stream

Input

`input` is a special function. You cannot define function like input in OJ.

Its return type is NOT-determined, but base on who gets the return value.

```
int a, b = input()
int arr[a]
# The input line will be splited by space and the items will be write into arr[0], arr[1], respectively.
arr = input()
arr[1:] = input()
```

Output

```
print a
print a, b
```

## Looping

```
for i in [1..100]
    print i
```

```
while {condition}
    # do something
```

## Functions

```
func = (x) ->
    # do something
    return 1
```

The input type will be guessed from the usage of this function. (If ambigious, the compiler will complain.)

You can also set the input type and default value.

```
func = (int x, int y = 10) ->
    # do something
```

All functions should have static return value. However you don't need to to specified it.
If there are multiple return statements in a function, their return types should matches.

Explicitly specify return type.

Sometimes it would be convenient to specify the function's return type,
e.g. when you want to cast the return value into `long` instead of `int`.

```
func = (x) -> (long)
    return 1
```

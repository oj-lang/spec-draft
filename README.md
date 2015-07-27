# Orange Juice Language Specifications

## Data Types

Basic: `int`, `long`, `bool`, `string`

Special: bigint, bigdec

Structure: array, queue, list(?), set, map

Define

```
int a
int a, b
int a[]
int a[100]
a = array<int>(100)
a = queue<int>
```

Self-define types

```
pair := int[2]
# or
pair := array<int>[2]
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
int a
int a[10]
```

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

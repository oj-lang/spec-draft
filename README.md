# Orange Juice Language Specifications

This is NOT a strict specification (yet). Just write down some thoughts on how this language should be.

## Data Types

### Basic

`int`, `long`, `bool`, `string`

Passed by value.

### Special

Predefined advanced data types.

bigint, bigdec

### Container

* `seq` - a sequence of items
* `set` - a sequence of unique items
* `map` - a dictionary of items

`seq` my be translated into different implemtation in C++.

| Index Access | Iterator Insert/Remove | Implementation |
|:------------:|:----------------------:|:--------------:|
| Any          | No                     | Vector         |
| No           | Yes                    | List           |
| Yes          | Yes                    | Deque          |

### Self-define types

From system-defined types.

```
pair := int[2]
# or
pair := seq<int>[2]
```

From attributes.

```
node :=
    x: int
    y: int
```

With methods.

```
circle :=
    x: int
    y: int
    r: int
    area: ->
        return PI * @r ^ 2
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
# A sequence with fixed length
int a[100]
# Same as above
a = seq<int>(100)
```

Implicitly declare of variables. In the example below, the type of result is defined by the return value of `func`.

```
result = func()
```

`result` will take the data type from function `func`.

## Input & output stream

`input` and `output` are special functions. You cannot define function like them in OJ.

### Input

Its return type is NOT-determined, but base on who gets the return value.

```
int a, b = input()
int arr[a]
# The input line will be splited by space and the items will be write into arr[0], arr[1], respectively.
arr = input()
arr[1:] = input()
```

### Output

```
print  # Print a blank line
print a
print a, b  # Space between a and b
print str(a) + str(b)  # No space between a and b
print a,  # No new line or space in the end.
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

```
int arr[100]  # A sequence of 100 items

for a in arr
    print a  ## Print all items in arr

for iter, a in arr
    # iter is an iterator of arr
    arr.remove(iter)  # Use of iterator in sequence modification is generally more efficient.

for index, iter, a in arr
    # index is a counter for the iteration. It starts from 0.
```

## Functions

### Define functions

#### Getting parameters

```
func = (x) ->
    return x ^ 2
```

Parameter type is optional. It will be guessed from usage.
If more then one usage occurs, the compiler will create overloading.

```
func = (int x, int y = 10) ->
    # do something
```

Optional parameters must be put after required parameters.

All functions should have static return value. However you don't need to to specified it.
If there are multiple return statements in a function, their return types should matches.

Explicitly specify return type.

Sometimes it would be convenient to specify the function's return type,
e.g. when you want to cast the return value into `long` instead of `int`.

```
func = (int x) -> (long)
    return 1
```

#### Setting return values

A function may have one or more return value. There are two ways to set return values.

First is to use return statements, shown as our example above.

Second is to declare return value in function signiture.

```
func = (int x) -> (long y)
    y = x * x
```

Return value can also have default value

```
func = (int x) -> (long y = 0)
    y = x * x
```

You can still use return statement in this case. If you change the return value from the left.

### Calling functions

Use `()` to call a function. If there is more than one paramaters, `()` is optional.

```
func()
func(a)
func a
```

### Pre-defined functions

* `len` - Length of variable. Reading from `len` method for self-defined types.
* `str` - The `to_str` value of variables.
* `int` - The `to_int` value of variables.
* `sort` - Sort the sequence.
* `copy` - Clone an object. It is built-in.

## Classes

Classes are just self defined types.

```
circle :=
    x: int
    y: int
    r: int
    area: -> (long)
        return PI * @r ^ 2
```

Initialize a class.

```
c = circle()
c.x = 100
cc = circle(x: 100)
```

### Constructor

```
circle :=
    x: int
    y: int
    r: int
    ctor: (int x, int y) ->
        @x = x
        @y = y
        @r = 10
    area: ->
        return PI * @r ^ 2
```

# Orange Juice Language Specifications

This is NOT a strict specification (yet). Just write down some thoughts on how this language should be.

## Data Types

### Basic

`int`, `long`, `bool`, `string`

Basic types will be passed by value. All other data types will be passed by reference.

### Special

Predefined advanced data types.

`BigInt`, `BigDec`

### Container

* `List` - a sequence of items
* `Set` - a sequence of unique items
* `Map` - a dictionary of items

`List` my be translated into different implemtation in C++.

| Index Access | Iterator Insert/Remove | Implementation |
|:------------:|:----------------------:|:--------------:|
| Any          | No                     | Vector         |
| No           | Yes                    | List           |
| Yes          | Yes                    | Deque          |

### Self-define types

From system-defined types.

From attributes.

```
class Node
    x: int
    y: int
```

With methods.

```
class Circle
    x: int
    y: int
    r: int
    area: ->
        return PI * @r ^ 2
```

Self defined types with methods are classes. They have inheritance. See classes section for detials.

### Pass by value

OJ always pass by value. For array, OJ will pass the pointer to the array. So modifying the array will
affect its content. You may wish to clone the array.

```
int a[100]
b = a.clone()
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
var a = List<int>(100)
# Defined type
var a = Node(100, 100)
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
int a, b
input a, b
```

### Output

```
print a, " ", b
print "%s %s" % (a, b)
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

for index, a in arr
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

## Classes

Classes are just self defined types.

```
Circle :=
    x: int
    y: int
    r: int
    area: -> (long)
        return PI * @r ^ 2
```

Initialize a class.

```
c = Circle()
c.x = 100
cc = Circle(x: 100)
```

### Constructor

```
Circle :=
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

### Inheritance

```
ColorCircle := Circle
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

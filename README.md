# Orange Juice Language Specifications

## Data Types

Basic: `int`, `long`, `bool`, `string`

Special: array, queue, list(?), set, map

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

## Input & output stream

Input

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

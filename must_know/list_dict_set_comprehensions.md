# List Comprehensions

## Table of Contents
* [List Comprehensions](#list-comprehensions)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
    * [Bad](#bad)
    * [Good](#good)
  * [Nested](#nested)
    * [Bad](#bad-1)
    * [Good](#good-1)
  * [Conditional](#conditional)
    * [Bad](#bad-2)
    * [Good](#good-2)
* [Dict Comprehensions](#dict-comprehensions)
  * [Basic](#basic-1)
    * [Bad](#bad-3)
    * [Good](#good-3)
* [Set Comprehensions](#set-comprehensions)
  * [Basic](#basic-2)
    * [Bad](#bad-4)
    * [Good](#good-4)

## Basic

### Bad

``` py
li = []
for i in range(10):
    li.append(i)

# li = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Good

``` py
li = [i for i in range(10)]

# li = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## Nested

### Bad

``` py
li = []
a = [0, 1]
b = ['a', 'b']
for i in a:
    for j in b:
        li.append((i, j))

# li = [(0, 'a'), (0, 'b'), (1, 'a'), (1, 'b')]
```

### Good

``` py
a = [0, 1]
b = ['a', 'b']
li = [(i, j) for i in a for j in b]

# li = [(0, 'a'), (0, 'b'), (1, 'a'), (1, 'b')]
```

## Conditional

### Bad

``` py
evens = []
for i in range(100):
    if i % 2 == 0:
        evens.append(i)

# evens = [0, 2, 4, 6, ..., 92, 94, 96, 98]
```

### Good

``` py
evens = [i for i in range(100) if i % 2 == 0]

# evens = [0, 2, 4, 6, ..., 92, 94, 96, 98]
```

# Dict Comprehensions

Comprehension can also be implemented on a dictionary object.

## Basic

Suppose we want to use a dictionary to store the length of each word.

### Bad

``` py
strings = ['abc', 'abcdefg']

d = {}
for s in strings:
    d[s] = len(s)

# d = {'abc': 3, 'abcdefg': 7}
```

### Good

``` py
strings = ['abc', 'abcdefg']
d = {s: len(s) for s in strings}

# d = {'abc': 3, 'abcdefg': 7}
```

# Set Comprehensions

Comprehension can also be implemented on a set object.

## Basic

Suppose we want to produce a set from 1 to 100, excluding multiples of 2 and 3.

### Bad

``` py
s = set()
for i in range(1, 101):
    if i % 2 != 0 and i % 3 != 0:
        s.add(i)

# s = {1, 5, 7, 11, 13, 17, 19, 23, 25, 29, 31, 35, 37, 41, 43, 47, 49, 53, 55, 59, 61, 65, 67, 71, 73, 77, 79, 83, 85, 89, 91, 95, 97}
```

### Good

``` py
s = {i for i in range(1, 101) if i % 2 != 0 and i % 3 != 0}

# s = {1, 5, 7, 11, 13, 17, 19, 23, 25, 29, 31, 35, 37, 41, 43, 47, 49, 53, 55, 59, 61, 65, 67, 71, 73, 77, 79, 83, 85, 89, 91, 95, 97}
```
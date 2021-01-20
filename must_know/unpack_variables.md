# Unpack variables

In python, there are several ways to assign **multiple values** (e.g., items of tuple, list) to **one variable** or **more than one variables**. We can even use the `*` and `**` symbols that we learned from [*args and **kwargs](args_kwargs.md) to indicate the variables.

## Table of Contents

* [Unpack variables](#unpack-variables)
  * [Table of Contents](#table-of-contents)
  * [Unpacking Iterables](#unpacking-iterables)
    * [Tuple](#tuple)
    * [String](#string)
    * [List](#list)
    * [Set](#set)
    * [Dict](#dict)
  * [Unpacking Generator](#unpacking-generator)
  * [Unpacking Function](#unpacking-function)
  * [Unpacking in For-Loops](#unpacking-in-for-loops)
  * [Unpacking with * Operator](#unpacking-with--operator)
    * [Iterable](#iterable)
    * [Generator](#generator)
    * [For-loops](#for-loops)
    * [Function (1)](#function-1)
    * [Function (2)](#function-2)
  * [Unpacking with ** Operator](#unpacking-with--operator-1)
    * [Combining dicts](#combining-dicts)
    * [WARN: Overlapping](#warn-overlapping)
* [Related Articles](#related-articles)


## Unpacking Iterables

### Tuple

``` py
tuples = 1, 2, 3
a, b, c = tuples  # 1, 2, 3
```

### String

``` py
a, b, c = "123"   # 1, 2, 3
a, b, c = "1234"  # ValueError: too many values to unpack (expected 3)
```

### List

``` py
a, b, c = [1, 2, 3]     # 1, 2, 3
a, b, c = [1, 2, 3, 4]  # ValueError: too many values to unpack (expected 3)
```

### Set

``` py
a, b, c = {1, 2, 3}     # 1, 2, 3
a, b, c = {1, 2, 3, 4}  # ValueError: too many values to unpack (expected 3)
```

### Dict

``` py
# Unpacking dict directly will only return keys
d = {"a": 1, "b": 2, "c": 3} 
a, b, c = d  # a, b, c

# Unpacking dict.values() will return values
a, b, c = d.values()  # 1, 2, 3


# Unpakcing dict.items() will return tuples of key-value pairs
a, b, c = d.items()
# (a, 1)
# (b, 2)
# (c, 3)
```

## Unpacking Generator

``` py
a, b, c = range(3)  # 0, 1, 2
a, b, c = range(4)  # ValueError: too many values to unpack (expected 3)
```

``` py
a, b, c = map(lambda x: x.upper(), "hey")  # H, E, Y
```

## Unpacking Function

``` py
def compute(i):
    return i, i ** 2, i ** 3


num, power, cube = compute(2)
num    # 2
power  # 4
cube   # 8
```

## Unpacking in For-Loops

``` py
sales = [("Pencil", 0.22, 1500), ("Notebook", 1.30, 550)]

for sale in sales:
    print(f"Total income for {sale[0]} is {sale[1]*sale[2]}")
    # Total income for Pencil is 330.0
    # Total income for Notebook is 715.0


for product, price, unit in sales:
    print(f"Total income for {product} is {price*unit}")
    # Total income for Pencil is 330.0
    # Total income for Notebook is 715.0
```

## Unpacking with * Operator

### Iterable

``` py
a, b, *_ = [1, 2, 3, 4, 5]
a  # 1 (int)
b  # 2 (int)
_  # [3, 4, 5] (list)
```

### Generator

``` py
first, *amid, last = map(lambda x: x**2, range(1, 10000))

first      # 1
last       # 99980001
len(amid)  # 9997
```

### For-loops

``` py
sales = [("Pencil", 0.22, 1500), ("Notebook", 1.30, 550)]

for product, *_ in sales:
    print(product, _)
    # Pencil [0.22, 1500]
    # Notebook [1.3, 550]
```

### Function (1)

``` py
def compute(i):
    return i, i ** 2, i ** 3

*_, cube = compute(3)
cube  # 27
```

### Function (2)

``` py
import sys
sys.version_info  # sys.version_info(major=3, minor=7, micro=7, releaselevel='final', serial=0)
major, minor, *_ = sys.version_info
major  # 3
minor  # 7
```

## Unpacking with ** Operator

### Combining dicts

``` py
number = {"one": 1, "two": 2}
letter = {"a": "A", "b": "B"}

combine = {**number, **letter}
combine  # {'one': 1, 'two': 2, 'a': 'A', 'b': 'B'}
```

### WARN: Overlapping

``` py
letter1 = {"a": "A", "b": "B"}
letter2 = {"a": "α", "b": "β"}

letter = {**letter1, **letter2}
letter  # {'a': 'α', 'b': 'β'}
```

# Related Articles

| Article                                           | Link                                                                   |
| ------------------------------------------------- | ---------------------------------------------------------------------- |
| 10 Python Tips and Tricks For Writing Better Code | https://youtu.be/C-gEQdGVXbk?t=839                                     |
| 7 More Tricks to Write Better Python Code         | https://youtu.be/SNTZpy0oDB8?t=605                                     |
| Unpacking in Python: Beyond Parallel Assignment   | https://stackabuse.com/unpacking-in-python-beyond-parallel-assignment/ |
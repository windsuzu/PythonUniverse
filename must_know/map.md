# Map

Before reading this article, please make sure you understand how the [lambda function](lambda_functions.md) works.

Like [zip()](zip.md) and [filter()](filter.md), map can create and return a generator. [generator](generator.md) is an implementation of iterator with **lazy evaluation features**, which can reduce memory usage very effectively.

## Table of Contents
* [Map](#map)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
    * [BONUS: List Comprehensions](#bonus-list-comprehensions)
  * [Multiple Iterables](#multiple-iterables)
    * [2 Lists](#2-lists)
    * [3 Lists](#3-lists)
    * [BONUS: Zip](#bonus-zip)

## Basic

map() performs the corresponding operation you give to all the elements in the iterable object. For example, in the following example, we replace each word in a string list with its corresponding character length.

``` py
li = ['a', 'apple', 'alphabet']
li = [*map(lambda x: len(x), li)]

# li = [1, 5, 8]
```

### BONUS: List Comprehensions

The above map() approach can actually be achieved using the [list comprehensions](list_dict_set_comprehensions.md) below.

``` py
li = ['a', 'apple', 'alphabet']
li = [len(s) for s in li]

# li = [1, 5, 8]
```

## Multiple Iterables

Map can operate on multiple lists at once.

### 2 Lists

Combine the elements of each position in the two lists.

``` py
num = [0, 1, 2]
li = ['a', 'apple', 'alphabet']
combined = [*map(lambda x, y: str(x) + y, num, li)]

# combined = ['0a', '1apple', '2alphabet']
```

### 3 Lists

Find the largest element in each position of the three lists.

``` py
num1 = [100, 1, 20]
num2 = [19, 4, 94]
num3 = [40, 6, 30]
m = [*map(lambda x, y, z: max(x, y, z), num1, num2, num3)]

# m = [100, 6, 94]
```

### BONUS: Zip

In fact, these implementation can also be achieved with the [zip() method](zip.md) and [list comprehension](list_dict_set_comprehensions.md).

``` py
num = [0, 1, 2]
li = ['a', 'apple', 'alphabet']
combined = [str(x) + y for (x, y) in zip(num, li)]
# combined = ['0a', '1apple', '2alphabet']


num1 = [100, 1, 20]
num2 = [19, 4, 94]
num3 = [40, 6, 30]
m = [max(tup) for tup in zip(num1, num2, num3)]
# m = [100, 6, 94]
```
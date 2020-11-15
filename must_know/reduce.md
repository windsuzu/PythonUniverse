# Reduce

Before reading this article, please make sure you understand how the [lambda function](lambda_functions.md) works.

## Table of Contents

* [Reduce](#reduce)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
    * [General Case](#general-case)
    * [Lambda Case](#lambda-case)

## Basic

reduce() recursively manipulates all the elements in a list and accumulates the results. This function is defined in `functools.reduce`.

### General Case

reduce() takes three parameters, the first is the operation function, the second is a iterable, and the third is the initial value. The first argument of the operation function is the cumulative value and the second argument is the current element of the list.

For example, we set the initial value to 100, and then subtracted values from the list, leaving 85.

``` py
from functools import reduce

def sub(x, y):
    return x - y

reduce(sub, [1, 2, 3, 4, 5], 100)  # 85
```

### Lambda Case

``` py
from functools import reduce

reduce(lambda x, y: x - y, [1, 2, 3, 4, 5], 100)  # 85
```
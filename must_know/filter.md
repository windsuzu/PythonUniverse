# Filter

Before reading this article, please make sure you understand how the [lambda function](lambda_functions.md) works.

Like [zip()](zip.md) and [map()](map.md), filter can create and return a generator. [generator](generator.md) is an implementation of iterator with **lazy evaluation features**, which can reduce memory usage very effectively.

## Table of Contents
* [Filter](#filter)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)

## Basic

The filter() function retrieves the desired value from the list and removes the unnecessary value. For example, in the following example we want to find the names of people whose names start with “O” in the list.

``` py
names = ['Liam', 'Olivia', 'Noah', 'Emma', 'Oliver', 'Ava']
choice = filter(lambda x: x.startswith('O'), names)

print(*choice, sep=', ')  # Olivia, Oliver
```
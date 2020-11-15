# Zip

Like [map()](map.md) and [filter()](filter.md), zip can create and return a generator. [generator](generator.md) is an implementation of iterator with **lazy evaluation features**, which can reduce memory usage very effectively.

## Table of Contents
* [Zip](#zip)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
  * [Unzip](#unzip)
  * [Uneven Lists](#uneven-lists)
    * [BONUS: Itertools.zip_longest](#bonus-itertoolszip_longest)
  * [Usage](#usage)

## Basic

zip() can combine elements of the same index from multiple lists so the combined object is in the tuple state.

``` py
a = [1, 2, 3]
b = [4, 5, 6]
c = [*zip(a, b)]

# c = [(1, 4), (2, 5), (3, 6)]
```

## Unzip

We can use the `zip(*zip_object)` syntax to achieve the unzip.

``` py
c = [(1, 4), (2, 5), (3, 6)]

print(list(zip(*c)))  # [(1, 2, 3), (4, 5, 6)]
```

## Uneven Lists

When the list is not the same length, the **shortest list** will be selected as the base.

``` py
a = [1, 2, 3]
b = [4, 5, 6, 8]
c = [100, 777, 999, 1213, 4456]
d = [*zip(a, b, c)]

# d = [(1, 4, 100), (2, 5, 777), (3, 6, 999)]
```

### BONUS: Itertools.zip_longest

If you want to use the longest list as a base and add padding to other list elements, use `itertools.zip_longest()` instead of zip().

``` py
from itertools import zip_longest

a = [1, 2, 3]
b = [4, 5, 6, 8]
c = [100, 777, 999, 1213, 4456]

d = [*zip_longest(a, b, c)]  # empty will be filled with None
# d = [(1, 4, 100), (2, 5, 777), (3, 6, 999), (None, 8, 1213), (None, None, 4456)]

d = [*zip_longest(a, b, c, fillvalue=0)]  # filled with 0
# d= [(1, 4, 100), (2, 5, 777), (3, 6, 999), (0, 8, 1213), (0, 0, 4456)]
```

## Usage

In machine learning model training, it is often necessary to shuffle the dataset, which can be achieved using the zip() function as described below.

``` py
import random

X = [1, 2, 3, 4, 5, 6]
y = [0, 1, 0, 0, 1, 1]
zipped_data = list(zip(X, y))  
# [(1, 0), (2, 1), (3, 0), (4, 0), (5, 1), (6, 1)]

random.seed(42)
random.shuffle(zipped_data)  
# [(4, 0), (2, 1), (3, 0), (5, 1), (1, 0), (6, 1)]

shuffled_zipped_data = map(list, zip(*zipped_data))
# map([4, 2, 3, 5, 1, 6], [0, 1, 0, 1, 0, 1])

new_X, new_y = shuffled_zipped_data
# new_X = [4, 2, 3, 5, 1, 6]
# new_y = [0, 1, 0, 1, 0, 1]
```
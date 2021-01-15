# Iterators terminating on the shortest input sequence

The `itertools` is a built-in module in Python 3 and is helpful for us to use a more pythonic way to manipulate the iterables (e.g., list, set, tuple, etc.). 

Another advantage of `itertools` is it also returns the [generator](../must_know/generator.md) type instances that have benefits of **lazy evaluation** from all its methods.

In this section, we will discuss the second part of `itertools`. The methods in this part all return a generator that generates finite items corresponding to your input.

## Table of Contents

* [Iterators terminating on the shortest input sequence](#iterators-terminating-on-the-shortest-input-sequence)
  * [Table of Contents](#table-of-contents)
  * [accumulate](#accumulate)
  * [chain](#chain)
  * [compress](#compress)
  * [filterfalse](#filterfalse)
  * [groupby](#groupby)
  * [islice](#islice)
  * [starmap](#starmap)
  * [takewhile](#takewhile)
  * [dropwhile](#dropwhile)
  * [zip_longest](#zip_longest)
* [Related Articles](#related-articles)

## accumulate

`accumulate` works like the [reduce](../must_know/reduce.md), but `accumulate` keep tracking the process of calculation and return in a generator.

This table takes [Python documentation #accumulate](https://docs.python.org/3/library/itertools.html#itertools.accumulate) as reference.

| Arguments                             | Results                              | Example                           |
| ------------------------------------- | ------------------------------------ | --------------------------------- |
| p (`iterable`), [, func=operator.add] | p[0], p[0]+p[1], p[0]+p[1]+p[2], ... | `accumulate([1, 2, 3]) = 1, 3, 6` |

``` py
import operator
from itertools import accumulate

gen = accumulate([1, 2, 3, 4])
list(gen)  # [1, 3, 6, 10]


gen = accumulate([1, 2, 3, 4], func=operator.mul)
list(gen)  # [1, 2, 6, 24]
```

## chain

This table takes [Python documentation #chain](https://docs.python.org/3/library/itertools.html#itertools.chain) as reference.

| Arguments          | Results                                      | Example                          |
| ------------------ | -------------------------------------------- | -------------------------------- |
| p, q (`iterables`) | p[0], p[1], ... p[-1], q[0], q[1], ... q[-1] | `chain("AB", "CD") = A, B, C, D` |

``` py
from itertools import chain

gen = chain([1, 2], [3, 4])
list(gen)  # [1, 2, 3, 4]


gen = chain("AB", "CD")
list(gen)  # [A, B, C, D]
```

## compress

This table takes [Python documentation #compress](https://docs.python.org/3/library/itertools.html#itertools.compress) as reference.

| Arguments                 | Results                             | Example                      |
| ------------------------- | ----------------------------------- | ---------------------------- |
| p, selector (`iterables`) | (p[0] if s[0]), (p[1] if s[1]), ... | `compress("AB", [0, 1]) = B` |

``` py
from itertools import compress

gen = compress([1, 2, 3], [1, 0, 1])
gen = compress([1, 2, 3], [True, False, True])  # same

list(gen)  # [1, 3]
```

## filterfalse

`filterfalse` is basically the opposite version of [filter](../must_know/filter.md).

This table takes [Python documentation #filterfalse](https://docs.python.org/3/library/itertools.html#itertools.filterfalse) as reference.

| Arguments            | Results      | Example                                           |
| -------------------- | ------------ | ------------------------------------------------- |
| pred, p (`iterable`) | p[i] != pred | `filterfalse(lambda x: x%2==0, [1, 2, 3]) = 1, 3` |

``` py
from itertools import filterfalse

gen = filterfalse(lambda x: x%2 ==0, [1, 2, 3])

list(gen)  # [1, 3]
```

## groupby

This table takes [Python documentation #groupby](https://docs.python.org/3/library/itertools.html#itertools.groupby) as reference.

| Arguments               | Results | Example |
| ----------------------- | ------- | ------- |
| p (`iterable`), [, key] |

``` py

```

## islice

<!-- just like slice function in list but islice returns generator -->

This table takes [Python documentation #islice](https://docs.python.org/3/library/itertools.html#itertools.islice) as reference.

| Arguments                                       | Results                             | Example                             |
| ----------------------------------------------- | ----------------------------------- | ----------------------------------- |
| p (`iterable`), [start=None], stop, [step=None] | p[start:stop:step] but in generator | `islice("ABCD", 0, None, 2) = A, C` |

``` py
gen = islice([1, 2, 3], 2)
list(gen)  # [1, 2]


gen = islice("ABCD", 2, 4)
list(gen)  # [C, D]


gen = islice("ABCD", 0, None, 2)
list(gen)  # [A, C]
```

## starmap

<!-- just like map function but it directly use the elements as func arguments -->

This table takes [Python documentation #starmap](https://docs.python.org/3/library/itertools.html#itertools.starmap) as reference.

| Arguments            | Results                       | Example                      |
| -------------------- | ----------------------------- | ---------------------------- |
| func, p (`iterable`) | func(*p[0]), ..., func(p[-1]) | `starmap(pow, [(2, 3), (2, 4)]) = 8, 16` |

``` py
from itertools import starmap

# with only one argument
gen = starmap(lambda x: x.lower(), "ABCD")
list(gen)  # [a, b, c, d]

# with 2 arguments
gen = starmap(lambda x, y: x + y, [(1, 2), (3, 4)])
list(gen)  # [3, 7]

# with different size of arugments
gen = starmap(lambda *keys: sum(keys) / len(keys), [[3, 8, 3], [4, 2]])
list(gen)  # [4.6666667, 3.0]
```

## takewhile

This table takes [Python documentation #takewhile](https://docs.python.org/3/library/itertools.html#itertools.takewhile) as reference.

| Arguments | Results | Example |
| --------- | ------- | ------- |


``` py

```

## dropwhile

This table takes [Python documentation #dropwhile](https://docs.python.org/3/library/itertools.html#itertools.dropwhile) as reference.

| Arguments | Results | Example |
| --------- | ------- | ------- |


``` py

```

## zip_longest

This table takes [Python documentation #zip_longest](https://docs.python.org/3/library/itertools.html#itertools.zip_longest) as reference.

| Arguments | Results | Example |
| --------- | ------- | ------- |


``` py

```


# Related Articles

| Article                                                                      | Link                                                             |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Python documentation - itertools                                             | https://docs.python.org/3/library/itertools.html                 |
| Python Tutorial: Itertools Module - Iterator Functions for Efficient Looping | https://www.youtube.com/watch?v=Qu3dThVy6KQ                      |
| Python 好用模組介紹 - itertools & more-itertools                             | https://myapollo.com.tw/zh-tw/python-itertools-more-itertools/   |
| Python標準庫之itertools庫的使用方法                                          | https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/364249/ |
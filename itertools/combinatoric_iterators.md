# Combinatoric Iterators

The `itertools` is a built-in module in Python 3 and is helpful for us to use a more pythonic way to manipulate the iterables (e.g., list, set, tuple, etc.). 

Another advantage of `itertools` is it also returns the [generator](../must_know/generator.md) type instances that have benefits of **lazy evaluation** from all of its methods.

In this section, we will discuss the third part of `itertools`. The methods in this section are all about the combinatoric methods in discrete mathematics.

## Table of Contents

* [Combinatoric Iterators](#combinatoric-iterators)
  * [Table of Contents](#table-of-contents)
  * [product](#product)
  * [permutations](#permutations)
  * [combinations](#combinations)
  * [combinations_with_replacement](#combinations_with_replacement)
* [Related Articles](#related-articles)

## product

This table takes [Python documentation #product](https://docs.python.org/3/library/itertools.html#itertools.product) as reference.

| Arguments               | Results                          | Example                                                        |
| ----------------------- | -------------------------------- | -------------------------------------------------------------- |
| `iterables`, `repeat=1` | cartesian products (nested-loop) | `product("ABC", repeat=2)= AA, AB, AC, BA, BB, BC, CA, CB, CC` |


``` py
from itertools import product

gen = product("AB", "CD")
list(gen)  # [AC, AD, BC, BD]


gen = product("AB", repeat=2)
list(gen)  # [AA, AB, BA, BB]


gen = product("AB", "CD", repeat=2)
list(gen)
# [ACAC, ACAD, ACBC, ACBD,
#  ADAC, ADAD, ADBC, ADBD,
#  BCAC, BCAD, BCBC, BCBD,
#  BDAC, BDAD, BDBC, BDBD]
```

## permutations

This table takes [Python documentation #permutations](https://docs.python.org/3/library/itertools.html#itertools.permutations) as reference.

| Arguments                     | Results                     | Example                                            |
| ----------------------------- | --------------------------- | -------------------------------------------------- |
| `iterable`, `r=len(iterable)` | permutation with length `r` | `permutations("ABC", r=2)= AB, AC, BA, BC, CA, CB` |

``` py
gen = permutations("ABC") # same as r=3
list(gen)  # [ABC, ACB, BAC, BCA, CAB, CBA]


gen = permutations("ABC", r=2)
list(gen)  # [AB, AC, BA, BC, CA, CB]


gen = permutations("ABC", r=1)
list(gen)  # [A, B, C]
```

## combinations

This table takes [Python documentation #combinations](https://docs.python.org/3/library/itertools.html#itertools.combinations) as reference.

| Arguments       | Results                     | Example                              |
| --------------- | --------------------------- | ------------------------------------ |
| `iterable`, `r` | combination with length `r` | `combinations("ABC", 2)= AB, AC, BC` |

``` py
gen = combinations("ABC", 1)
list(gen)
# [A, B, C]


gen = combinations("ABC", 2)
list(gen)
# [AB, AC, BC]


gen = combinations("ABC", 3)
list(gen)
# [ABC]
```

## combinations_with_replacement

This table takes [Python documentation #combinations_with_replacement](https://docs.python.org/3/library/itertools.html#itertools.combinations_with_replacement) as reference.

| Arguments       | Results                                           | Example                                                           |
| --------------- | ------------------------------------------------- | ----------------------------------------------------------------- |
| `iterable`, `r` | combination with length `r` and repeated elements | `combinations_with_replacement("ABC", 2)= AA, AB, AC, BB, BC, CC` |

``` py
gen = combinations_with_replacement("ABC", 1)
list(gen)
# [A, B, C]


gen = combinations_with_replacement("ABC", 2)
list(gen)
# [AA, AB, AC, 
#  BB, BC, 
#  CC]


gen = combinations_with_replacement("ABC", 3)
list(gen)
# [AAA, AAB, AAC, ABB, ABC, ACC,
#  BBB, BBC, BCC,
#  CCC]
```


# Related Articles

| Article                                                                      | Link                                                             |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Python documentation - itertools                                             | https://docs.python.org/3/library/itertools.html                 |
| Python Tutorial: Itertools Module - Iterator Functions for Efficient Looping | https://www.youtube.com/watch?v=Qu3dThVy6KQ                      |
| Python 好用模組介紹 - itertools & more-itertools                             | https://myapollo.com.tw/zh-tw/python-itertools-more-itertools/   |
| Python標準庫之itertools庫的使用方法                                          | https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/364249/ |
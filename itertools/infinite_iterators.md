# Infinite Iterators

The `itertools` is a built-in module in Python 3 and is helpful for us to use a more pythonic way to manipulate the iterables (e.g., list, set, tuple, etc.). 

Another advantage of `itertools` is it also returns the [generator](../must_know/generator.md) type instances that have benefits of **lazy evaluation** from all its methods.

In this section, we will discuss the first part of `itertools`. The methods in this part all return a generator that generates an infinite number of items and won't stop.

## Table of Contents

* [Infinite Iterators](#infinite-iterators)
  * [Table of Contents](#table-of-contents)
  * [count](#count)
  * [cycle](#cycle)
  * [repeat](#repeat)
* [Related Articles](#related-articles)

## count

This table takes [Python documentation #count](https://docs.python.org/3/library/itertools.html#itertools.count) as reference..

| Arguments       | Results                             | Example                                |
| --------------- | ----------------------------------- | -------------------------------------- |
| start, [step=1] | start, start+step, start+2step, ... | `count(2.5, 0.5) = 2.5 3.0 3.5 4.0...` |


``` py
from itertools import count 

gen = count(2.5, 0.5)

for x in gen:
    print(x)
    # 2.5, 3.0, 3.5, 4.0, ... non-stop
```

## cycle

This table takes [Python documentation #cycle](https://docs.python.org/3/library/itertools.html#itertools.cycle) as reference.

| Arguments      | Results                              | Example                            |
| -------------- | ------------------------------------ | ---------------------------------- |
| p (`iterable`) | p[0], p[1], ... p[-1], p[0], p[1]... | `cycle([1, 2, 3]) = 1 2 3 1 2 ...` |

``` py
from itertools import cycle 

gen = cycle([1, 2, 3])

for x in gen:
    print(x)
    # 1, 2, 3, 1, 2, ... non-stop
```

## repeat

This table takes [Python documentation #repeat](https://docs.python.org/3/library/itertools.html#itertools.repeat) as reference.

| Arguments      | Results                                        | Example                           |
| -------------- | ---------------------------------------------- | --------------------------------- |
| item, [n=None] | item, item, item, … endlessly or up to n times | `repeat(Cat(), 2) = Cat(), Cat()` |

``` py
from itertools import repeat 

class Cat:
    ...
    
gen = repeat(Cat(), 2)

for cat in gen:
    print(cat)
    # <__main__.Cat object at 0x0000019AC1C5D348>
    # <__main__.Cat object at 0x0000019AC1C5D348>
```

# Related Articles

| Article                                                                      | Link                                                             |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Python documentation - itertools                                             | https://docs.python.org/3/library/itertools.html                 |
| Python Tutorial: Itertools Module - Iterator Functions for Efficient Looping | https://www.youtube.com/watch?v=Qu3dThVy6KQ                      |
| Python 好用模組介紹 - itertools & more-itertools                             | https://myapollo.com.tw/zh-tw/python-itertools-more-itertools/   |
| Python標準庫之itertools庫的使用方法                                          | https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/364249/ |
# Counter

The Counter is a subclass of `dict`, as are [defaultdict](defaultdict.md) and [OrderedDict](ordereddict.md).

It is designed to count iterables such as strings, lists, dictionaries, etc.

## Table of Contents

* [Counter](#counter)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
  * [update()](#update)
  * [elements()](#elements)
  * [most_common(int)](#most_commonint)
  * [subtract()](#subtract)
  * [Magic method](#magic-method)
* [Related Articles](#related-articles)

## Basic

There are several ways to initialize a `Counter` object. For example:

1. You can count every **character** from a string.
2. You can count every **item** in a list.
3. You can initialize the `Counter` with an existed dict.
4. You can initialize the `Counter` with **keyword arguments**.

``` py
c = Counter('gallahad')
# Counter({'a': 3, 'l': 2, 'g': 1, 'h': 1, 'd': 1})

c = Counter(["apple", "apple", "banana"])
# Counter({'apple': 2, 'banana': 1})

c = Counter({'red': 4, 'blue': 2})
# Counter({'red': 4, 'blue': 2})

c = Counter(cats=4, dogs=8)
# Counter({'dogs': 8, 'cats': 4})
```

The default value for elements that are not counted is 0.

``` py
c = Counter('gallahad')
c["e"]  # 0
```

## update()

You can add values to the `Counter` by using `update()` method.

``` py
c = Counter(cats=4, dogs=8)

c.update(birds=10)
# Counter({'cats': 4, 'dogs': 8, 'birds': 10})
```

## elements()

The method `elements()` will return an iterator that outputs all the elements from the `Counter` in the order first encountered.

``` py
c = Counter(cats=4, dogs=8)
list(c.elements())
# ['cats', 'cats', 'cats', 'cats', 'dogs', 'dogs', 'dogs', 'dogs', 'dogs', 'dogs', 'dogs', 'dogs']
```

## most_common(int)

The method `most_common(n: int)` will return a list of top `n` key-value pairs that have been counted the most times.

If `n` > `len(counter)` OR `n` is omitted or `None`, it will return a list of all elements.

``` py
c = Counter(cats=4, dogs=8)
c.most_common(1)  # [('dogs', 8)]
c.most_common(2)  # [('dogs', 8), ('cats', 4)]
c.most_common(3)  # [('dogs', 8), ('cats', 4)]
c.most_common()   # [('dogs', 8), ('cats', 4)]
```

## subtract()

The method `subtract` can do the subtraction for two `Counter`s, and the results of counts can become negative.

``` py
c = Counter(cats=4, dogs=8)
d = Counter(cats=5, dogs=3)

c.subtract(d)  # Counter({'cats': -1, 'dogs': 5})
```

In the contrast, you can also use the [magic method](../must_know/magic_method.md) `__sub__ (-)` to do the subtraction, but this will remove the elements whose count is less than zero.

``` py
c = Counter(cats=4, dogs=8)
d = Counter(cats=5, dogs=3)

c - d  # Counter({'dogs': 5})
```

## Magic method

`Counter` has built-in [magic methods](../must_know/magic_method.md) for `add`, `subtract`, `intersect` and `union`.

* add: `c[x] + d[x]`
* sub: `c[x] - d[x]` (keeping only positive counts)
* intersect: `min(c[x], d[x])`
* union: `max(c[x], d[x])`

``` py
c = Counter(cats=4, dogs=8)
d = Counter(cats=5, dogs=3)

c + d  # Counter({'cats': 9, 'dogs': 11})
c - d  # Counter({'dogs': 5})
c & d  # Counter({'cats': 4, 'dogs': 3})
c | d  # Counter({'cats': 5, 'dogs': 8})
```

# Related Articles

| Article                                    | Link                                                                   |
| ------------------------------------------ | ---------------------------------------------------------------------- |
| collections - Counter                      | https://docs.python.org/3/library/collections.html#collections.Counter |
| Python Counter in Collections with Example | https://www.guru99.com/python-counter-collections-example.html         |
| 7 More Tricks to Write Better Python Code  | https://youtu.be/SNTZpy0oDB8?list=LL&t=1609                            |
# OrderedDict

OrderedDict is a subclass of `dict`, just like [defaultdict](defaultdict.md), but `OrderedDict` can be sorted by insertion order, just like we do `append()` in a `list`.

## Table of Contents

* [OrderedDict](#ordereddict)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
  * [Sort Combination](#sort-combination)
  * [Popitem](#popitem)
  * [Move_to_end](#move_to_end)
  * [Custom OrderedDict](#custom-ordereddict)
  * [OrderedCounter](#orderedcounter)
* [Related Articles](#related-articles)

## Basic

The first thing to do is to initialize the `OrderedDict`, there are several ways to implement it, and here is a demonstration to initialize the `OrderedDict` with [zip](../must_know/zip.md) and [dict comprehension](../must_know/list_dict_set_comprehensions.md).

``` py
from collections import OrderedDict

location = ["C", "B", "A"]
population = [32, 46, 12]

d = OrderedDict({l: p for l, p in zip(location, population)})
# OrderedDict([('C', 32), ('B', 46), ('A', 12)])
```

The newly inserted `key-value pairs` will be stacked at the end of the `OrderedDict`, and the pair that is simply modified will be left in place.

``` py
d["D"] = 44
d["E"] = 52
# OrderedDict([('C', 32), ('B', 46), ('A', 12), ('D', 44), ('E', 52)])

d["B"] = 40
# OrderedDict([('C', 32), ('B', 40), ('A', 12), ('D', 44), ('E', 52)])
```

## Sort Combination

It's good to use `sorted()` when we initialize the `OrderedDict` because the `OrderedDict` has the power to stored the order of items.

``` py
d = {l: p for l, p in zip(location, population)}

d = OrderedDict(sorted(d.items(), key=lambda x: x[0]))
# OrderedDict([('A', 12), ('B', 46), ('C', 32)])

d = OrderedDict(sorted(d.items(), key=lambda x: x[1]))
# OrderedDict([('A', 12), ('C', 32), ('B', 46)])
```

## Popitem

We can use the built-in method `popitem(last=bool)` to pop the items from the `OrderedDict`, it will pop the items in `Last-In-First-Out` style if the default parameter `last=True`, else it will pop the item in `First-In-First-Out` style. 

``` py
# d = OrderedDict([('C', 32), ('B', 40), ('A', 12), ('D', 44), ('E', 52)])

d.popitem()  # ('E', 52)
# OrderedDict([('C', 32), ('B', 40), ('A', 12), ('D', 44)])

d.popitem(False)  # ('C', 32)
# OrderedDict([('B', 40), ('A', 12), ('D', 44)])
```

## Move_to_end

`move_to_end(key, last=True)` will move the item to the **end** of the `OrderedDict`, and if `last=False`, it will move the item to the **beginning**.

``` py
# d = OrderedDict([('C', 32), ('B', 40), ('A', 12), ('D', 44), ('E', 52)])

d.move_to_end("C")
# OrderedDict([('B', 40), ('A', 12), ('D', 44), ('E', 52), ('C', 32)])

d.move_to_end("D", last=False)
# OrderedDict([('D', 44), ('B', 40), ('A', 12), ('E', 52), ('C', 32)])
```

## Custom OrderedDict

We can always move the items to the end of the `OrderedDict` when we modify the existing ones, instead of staying them in place.

``` py
class LastUpdatedOrderedDict(OrderedDict):
    def __setitem__(self, key, value):
        if key in self:
            del self[key]
        OrderedDict.__setitem__(self, key, value)


d = {l: p for l, p in zip(location, population)}
d = LastUpdatedOrderedDict(d)
# LastUpdatedOrderedDict([('C', 32), ('B', 46), ('A', 12)])

d["C"] = 33
# LastUpdatedOrderedDict([('B', 46), ('A', 12), ('C', 33)])
```

## OrderedCounter

An ordered dictionary can be combined with the [Counter](counter.md) class so that the counter **remembers the order** elements are **first encountered**.

``` py
from collections import OrderedDict, Counter

class OrderedCounter(Counter, OrderedDict):
    'Counter that remembers the order elements are first encountered'

    def __repr__(self):
        return '%s(%r)' % (self.__class__.__name__, OrderedDict(self))

    def __reduce__(self):
        return self.__class__, (OrderedDict(self),)


s = "daaaabbccddcd"
OrderedCounter(s)
# OrderedCounter(OrderedDict([('d', 4), ('a', 4), ('b', 2), ('c', 3)]))
```

# Related Articles

| Article                                   | Link                                                                                           |
| ----------------------------------------- | ---------------------------------------------------------------------------------------------- |
| collections - OrderedDict objects  | https://docs.python.org/3.4/library/collections.html?highlight=ordereddict#ordereddict-objects |
| How do I sort a dictionary by value?      | https://stackoverflow.com/questions/613183/how-do-i-sort-a-dictionary-by-value                 |
| collections之OrderedDict                  | https://zhuanlan.zhihu.com/p/110407087                                                         |
| 7 More Tricks to Write Better Python Code | https://youtu.be/SNTZpy0oDB8?list=LL&t=1178                                                    |
# _ (private) vs. __ (name mangling)

In python, although there is no full implementation of `private` or `protected` as in java, but a `single underscore` can be used to achieve an effect similar to `private`. 

In addition, the use of `double underscores` is intended to **avoid conflicts between parent and child variables**, not for the effect of `private`. This conflict resolved by `double underscore` is also known as **name mangling**.

For a more detailed explanation, please refer to the official documentation: [9.6. Private Variables](https://docs.python.org/3/tutorial/classes.html#private-variables)

## Table of Contents

* [_ (private) vs. __ (name mangling)](#_-private-vs-__-name-mangling)
  * [Table of Contents](#table-of-contents)
  * [_ (Private)](#_-private)
  * [__ (Name Mangling)](#__-name-mangling)
* [Related Articles](#related-articles)

## _ (Private)

According to the documentation, there is no functionality of **private** in python, but there is a "convention" to add a `single underscore` in front of a variable to represent that the variable is "**private**".

At this point a name prefixed with an underscore (e.g. `_variable`) should be treated as a **non-public part of the API**, whether it is a variable, or a method, or a class.

So objects preceded by a variable name with a `single underscore` can still be executed as usual.

``` py
# > test.py
class _Dog:
    _weight = 5

    def _bark(self):
        print("bark")


def _hello():
    print("hi")


dog = _Dog()
print(dog._weight)  # 5
dog._bark()         # bark
_hello()            # hi
```

It is worth mentioning that when `from import *` is used in other files, these "private" objects are blocked from use.

``` py
# > other.py
from test import *

dog = _Dog() # NameError: name '_Dog' is not defined
_hello()     # NameError: name '_hello' is not defined
```

But it is possible to use these "private" objects by using `import` with filename, or by specifying the variables in `from import`.

``` py
# > other.py

import test

dog = test._Dog()
dog._bark()    # bark
test._hello()  # hi
```

``` py
# > other.py

from test import _Dog, _hello

dog = _Dog()
dog._bark()  # bark
_hello()     # hi
```

## __ (Name Mangling)

Two leading underscores (e.g. `__variable`) is a mechanism for solving `naming mangling` (avoid name clashes of names with names defined by subclasses). A variable with two leading underscores added will be bound to the classname, creating a new variable name. (e.g., `__variable` to `_classname__variable`)

``` py
class Dog:
    __weight = 5
    weight = 1

print(dir(Dog))
# ['_Dog__weight', '__class__', '__delattr__', '__dict__', ..., weight]
```

The usage is as follows, when the variable name of a subclass duplicates the parent, you can distinguish the two by `two leading underscores`.

...

I couldn't think of any time I could use this mechanism, so I just copied and pasted the official example. hahahaha ...

``` py
class Mapping:
    def __init__(self, iterable):
        self.items_list = []
        self.__update(iterable)

    def update(self, iterable):
        for item in iterable:
            self.items_list.append(item)

    __update = update   # private copy of original update() method


class MappingSubclass(Mapping):
    def update(self, keys, values):
        # provides new signature for update() but does not break __init__()
        for item in zip(keys, values):
            self.items_list.append(item)
```

> The above example would work even if `MappingSubclass` were to introduce a `__update` identifier since it is replaced with `_Mapping__update` in the Mapping class and `_MappingSubclass__update` in the MappingSubclass class respectively.


# Related Articles

| Article                                 | Link                                                                                        |
| --------------------------------------- | ------------------------------------------------------------------------------------------- |
| Python中的underscore _ 與 __ 及實例剖析 | https://medium.com/bits-to-blocks/python%E4%B8%AD%E7%9A%84underscore-%E8%88%87-9b40caf32483 |
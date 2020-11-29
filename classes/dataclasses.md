# Dataclasses

Has this ever happened to you? Creating a class with a lot of parameters, and you need to initialize one by one manually.

``` py
class Product(object):
    def __init__(self, id, author_id, category_id, brand_id, spu_id, 
                 title, item_id, n_comments, creation_time, update_time, 
                 source='', parent_id=0, ancestor_id=0):
        
        self.id = id
        self.author_id = author_id
        ...
```

Sometimes you also have to write a `__repr__` or `__str__` to express the classes with these variables, or `__eq__`, `__gt__` to compare the classes. This is very annoying and tedious, so python provides a [dataclasses module](https://docs.python.org/3/library/dataclasses.html) in version 3.7 to simplify the process in building classes.

## Table of Contents

* [Dataclasses](#dataclasses)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
  * [Post Init](#post-init)
  * [Field](#field)
  * [InitVar](#initvar)
* [Related Articles](#related-articles)

## Basic

`dataclasses` will automatically add `__repr__`, `__eq__` and other [magic methods](../must_know/magic_method.md) for us. Just install and import the `dataclasses` module and add the `dataclass` decorator to the class.

``` py
from dataclasses import dataclass

@dataclass
class InventoryItem:
    name: str
    unit_price: float
    quantity_on_hand: int = 0

    def total_cost(self) -> float:
        return self.unit_price * self.quantity_on_hand

item = InventoryItem("product", 100, 1)
print(item)  # InventoryItem(name='product', unit_price=100, quantity_on_hand=1)
```

<!-- TODO: add links to the explaination of annotations, typing -->

You can see that the class of each variable is marked with `variable: type`, which is python 3 [function annotations](). The [typing]() module that helps annotations will also be used later on.

## Post Init

There are some variables that we want to change in `__init__`, so dataclasses provides a `__post_init__` function to do that.

``` py
from dataclasses import dataclass

@dataclass
class InventoryItem:
    name: str
    unit_price: float
    quantity_on_hand: int = 0

    def __post_init__(self):
        self.unit_price *= 1.1
```

## Field

`dataclasses` provides a `field()` method to initialize each variable differently. The parameters to `field()` are:

- `default`: default value
- `default_factory`: zero-argument callable used to define default value
- `init`: bool, indicates whether this variable should be put into `__init__` or not.
- `compare`: bool, indicates whether this variable should be put into a comparable magic method such as `__eq__`, `__gt__`, etc.


``` py
from dataclasses import dataclass, field
from typing import List

@dataclass
class InventoryItem:
    name: str
    unit_price: float = field(default=0.0)
    quantity_on_hand: int = field(default=0, repr=False)
    parts: List[str] = field(default_factory=list)


item = InventoryItem("product")
print(item)  # InventoryItem(name='product', unit_price=0.0, parts=[])
```

## InitVar

`dataclasses` also provides variables that only appear in `__post_init__` and don't really become class or instance variables. Just define the variable as `InitVar` and pass it as `__post_init__`.

``` py
from dataclasses import InitVar, dataclass, field
from typing import List


@dataclass
class InventoryItem:
    name: str
    unit_price: float = field(default=0.0)
    quantity_on_hand: int = field(default=0, repr=False)
    parts: List[str] = field(default_factory=list)
    parts_number: InitVar[int] = 0

    def __post_init__(self, parts_number):
        self.parts.extend([f"part{i}" for i in range(1, parts_number + 1)])


item = InventoryItem("product", parts_number=2)
print(item)  # InventoryItem(name='product', unit_price=0.0, parts=['part1', 'part2'])
```

# Related Articles

| Article                                                     | Link                                        |
| ----------------------------------------------------------- | ------------------------------------------- |
| attrs 和 Python3.7 的 dataclasses                           | https://zhuanlan.zhihu.com/p/34963159       |
| Using Python dataclasses to simplify managing class objects | https://www.youtube.com/watch?v=FcVCfGJrkUQ |
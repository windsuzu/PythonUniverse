# NamedTuple

NamedTuple is a more readable tuple, it can have names for itself and its elements. 

``` py
# tuple
point = (1, 2)
point[0]  # 1
point[1]  # 2


# namedtuple (init like a class)
Point = namedtuple("Point", ["x", "y"])

point = Point(1, 2)
point[0]  # 1
point[1]  # 2

point.x   # 1
point.y   # 2
```

## Table of Contents

* [NamedTuple](#namedtuple)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
  * [_make()](#_make)
  * [_asdict()](#_asdict)
  * [_replace()](#_replace)
  * [_fields](#_fields)
* [Related Articles](#related-articles)

## Basic

The first thing we need to do is to define a `namedtuple` object by giving its `name` and `features`. 

1. `name`: string
2. `features`: 
   1. an iterable
   2. a string that divides the features with comma
   3. from other `namedtuple` using the attribute [_fields](#_fields)

``` py
# 1
Dog = namedtuple("Dog", ["name", "age"])


# 2
Dog = namedtuple("Dog", "name, age")


# 3
Other = namedtuple("Other", "name, age")
Other._fields  # ("name", "age")
Dog = namedtuple("Dog", [*Other._fields, "height"])
```

## _make()

`_make` is a class method that makes a new instance from an existing sequence or iterable.

``` py
Dog = namedtuple("Dog", "name, age")

# from list
feature_list = ["happy", 3]
Dog._make(feature_list)


# from tuple #1
feature_tuple = ("happy", 3)
Dog._make(feature_tuple)


# from tuple #2
features = "happy", 3
Dog._make(features)


# from dict values
feature_dict = {"name": "happy", "age": 3}
Dog._make(feature_dict.values())
```

## _asdict()

`_asdict` is a class method that converts the current `namedtuple` into an `OrderedDict` instance (in Python 3.8).

``` py
Dog = namedtuple("Dog", "name, age")
dog = Dog("happy", 3)
dog._asdict()  # OrderedDict([('name', 'happy'), ('age', 3)])
```

## _replace()

`_replace` is a class method that returns a new `namedtuple` replacing specified features with new values.

``` py
Dog = namedtuple("Dog", "name, age")
dog = Dog("happy", 3)
dog = dog._replace(age=5)  # Dog(name='happy', age=5)
```

## _fields

`_fields` is a class attribute, it will return a tuple of strings listing the features.

``` py
Dog = namedtuple("Dog", "name, age")
Dog._fields  # ("name", "age")

dog = Dog("happy", 3)
dog._fields  # ("name", "age")
```

# Related Articles

| Article                                  | Link                                                                                                        |
| ---------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| collections - namedtuple()               | https://docs.python.org/3/library/collections.html#namedtuple-factory-function-for-tuples-with-named-fields |
| The Complete Python Course For Beginners | https://youtu.be/sxTmJE4k0ho?list=LL&t=15915                                                                |
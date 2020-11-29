# Abstract Class

The `abstract class` and `interface` are widely used in software design, mainly for implementing the most important [polymorphism](https://en.wikipedia.org/wiki/Polymorphism_(computer_science)). Python also provides an `abc (Abstract Base Classes)` module for us to implement abstract classes. For more information, see [abc — Abstract Base Classes — Python 3.9.1rc1 documentation](https://docs.python.org/3/library/abc.html)

## Table of Contents

* [Abstract Class](#abstract-class)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
    * [Soft version](#soft-version)
    * [Hard version](#hard-version)
  * [abc module](#abc-module)
    * [Passing metaclass](#passing-metaclass)
    * [ABC class helper](#abc-class-helper)
  * [abc with other decorators](#abc-with-other-decorators)

## Basic

There are two ways to implement an abstract class in Python: one is to issue an error when dynamically discovering that the abstract has not been implemented, which is the **soft version**, and the other is to check that the abstract has not been implemented at the time the class is created, which is the **hard version**.

### Soft version

There is no use of `abc` module in soft version, just use `NotImplementedError` to alert user.

``` py
class Base(object):
    def do(self):
        raise NotImplementedError("Please Implement this method")


class Derived(Base):
    pass


d = Derived()  # nothing happened

...

d.do()         # NotImplementedError: Please Implement this method
```

### Hard version

In the hard version, `abc` module is used. This time, you don't even need to write `NotImplementedError`, as long as the subclass doesn't implement abstract methods, an error will occur.

``` py
from abc import ABC, abstractmethod

class Base(ABC, object):
    @abstractmethod
    def do(self):
        pass


class Derived(Base):
    pass


d = Derived()  # TypeError: Can't instantiate abstract class Derived with abstract methods do
```

## abc module

Now let's talk more about abc module. There are two ways to introduce an abc module to implement an abstract class:

1. Passing the [metaclass](../must_know/metaclasses.md) keyword and using `ABCMeta` directly.
2. A helper class `ABC` that has ABCMeta as its metaclass.

Regardless of the method you use, you then need to add the [decorator](../must_know/closure_decorator.md) `@abstractmethod` to the header of the function that you specify as abstract.

### Passing metaclass

To use the metaclass method, the `metaclass` must be placed at the end of the class bases as a **keyword argument**.

``` py
from abc import ABCMeta, abstractmethod

class Base(object, metaclass=ABCMeta):
    @property
    def foo(self):
        return 10

    @abstractmethod
    def do(self):
        pass


class Derived(Base):
    def do(self):
        print('do')


d = Derived()
print(d.foo)  # 10
d.do()        # do
```

### ABC class helper

To use the class helper method, the `ABC class` must be placed first in the class bases as the **first successor object**.

``` py
from abc import ABC, abstractmethod

class Base(ABC, object):
    @property
    def foo(self):
        return 10

    @abstractmethod
    def do(self):
        pass


class Derived(Base):
    def do(self):
        print('do')


d = Derived()
print(d.foo)  # 10
d.do()        # do
```

Abstract class can also have inheritance effect, so `foo` can be used in subclasses.

## abc with other decorators

In the above example, `foo` is a property, which can also be abstracted. Not only [property](property_getter_setter.md), we can abstract [classmethod, static method](method_class_static.md) as well.

After python 3.3, python provides **nested decorator** methods to implement abstraction of `property`, `setter`, `classmethod`, `staticmethod`, and so on. 

The approach is simple, just add `@abstractmethod` to the original decorator!

``` py
class C(ABC):
    @abstractmethod
    def my_abstract_method(self, ...):
        ...

    @classmethod
    @abstractmethod
    def my_abstract_classmethod(cls, ...):
        ...

    @staticmethod
    @abstractmethod
    def my_abstract_staticmethod(...):
        ...

    @property
    @abstractmethod
    def my_abstract_property(self):
        ...

    @my_abstract_property.setter
    @abstractmethod
    def my_abstract_property(self, val):
        ...

    @abstractmethod
    def _get_x(self):
        ...

    @abstractmethod
    def _set_x(self, val):
        ...
```

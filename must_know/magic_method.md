# Magic Method

Magic method is also known as **dunder method** or **data model method**, the most basic use is to implement the `__init__`, `__repr__`, `__str__` and other class builtin functions or plus sign `+`, multiplication sign `*`, greater than `>=`, less than `<=` and other symbolic calculations.

## Table of Contents

* [Magic Method](#magic-method)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
    * [Class Magic Method](#class-magic-method)
    * [Numerical, Comparison Magic Method](#numerical-comparison-magic-method)
    * [Representation Magic Method](#representation-magic-method)
    * [Callable Magic Method](#callable-magic-method)
    * [Iterable Magic Method](#iterable-magic-method)
    * [Context Manager Magic Method](#context-manager-magic-method)
* [Related Articles](#related-articles)

## Basic

The naming format of the magic method is represented by two underlines in front and back. For example, summing two integers is in fact a way to implement `__add__` on the int class. 

All magic methods can be found in the Python [Data Model](https://docs.python.org/3/reference/datamodel.html) documentation.

For example, we can add two int's and change the result to concatenation.

``` py
class my_int(int):
    def __add__(self, x):
        return int(f"{self}{x}")

a = my_int(1)
print(a + 3)  # 13
```

### Class Magic Method

When creating a class, we often use `__init__` to give the class some variables. But there is a function that is executed before `__init__`, called `__new__`.

1. `__new__`: **It's an class level method**, mainly used when you want to inherit immutable classes such as `str`, `int`, etc., or when you want to implement [custom metaclasses](metaclasses.md). The introduction of metaclasses can be viewed by clicking on the link! 
2. `__init__`: It is called only when the constructor is executed and is used to add attributes. **It's an instance level method**.
3. `__del__`: It is triggered when an instance is to be deleted or recycled.

Below I create a `BinaryInt` that automatically turns numbers into binary strings.

``` py
class BinaryInt(str):
    def __new__(cls, val):
        print(f"__new__: '{val}' -> binary int -> '{val:b}'")
        return str.__new__(cls, f"{val:b}")

    def __init__(self, val):
        print("__init__:", self)

    def __del__(self):
        print("__del__:", self)
        del self


a = BinaryInt(5)
print('a:', a)

# __new__: '5' -> binary int -> '101'
# __init__: 101
# a: 101
# __del__: 101
```

### Numerical, Comparison Magic Method

With magic method, we can take some of the non-comparable or non-calculable custom classes and make them comparable and calculable.

For example, we create a class `Person`, and then use age to compare and calculate between the `Person`s.

``` py
class Person:
    def __init__(self, age):
        self.age = age

    def __add__(self, person):
        return self.age + person.age

    def __sub__(self, person):
        return self.age - person.age

    def __mul__(self, person):
        return self.age * person.age

    def __truediv__(self, person):
        return self.age / person.age

    def __floordiv__(self, person):
        return self.age // person.age

    def __eq__(self, person):
        return self.age == person.age

    def __gt__(self, person):
        return self.age > person.age

    def __ge__(self, person):
        return self.age >= person.age

    def __lt__(self, person):
        return self.age < person.age

    def __le__(self, person):
        return self.age <= person.age


a = Person(15)
b = Person(30)
print(a + b)  # 45
print(a > b)  # False
print(sorted([b, a]))  # [a, b]
```

### Representation Magic Method

There are two ways of expressing classes, one is `__repr__` and the other is `__str__`. 

Very many people have different opinions about the difference between the two, But to put it bluntly, I would say `__repr__` is for **developers** and `__str__` is for **customers**.

``` py
class Person:
    def __init__(self, age):
        self.age = age
    
    def __str__(self):
        return f"A Person who is {self.age} year(s) old"
    
    def __repr__(self):
        return f"Person(age={self.age})"


a = Person(15)
print(a)  # A Person who is 15 year(s) old
print(repr(a))  # Person(age=15)
print([a])  # [Person(age=15)]
```

### Callable Magic Method

Defining `__call__` for a class allows the class to take arguments and turn them into something like a function that can be called.

``` py
class Person:
    def __init__(self, age):
        self.age = age

    def __call__(self):
        print(f"I'm {self.age}")


a = Person(15)
b = Person(30)

a()  # I'm 15
b()  # I'm 30
```

### Iterable Magic Method

We can also use the magic method to customize an iterable object with arbitrary rules.

1. `__len__`: Define the length of your iterable, can be obtained with `len()`.
2. `__getitem__`: same as `self[key]`
3. `__setitem__`: same as `self[key] = val`
4. `__iter__`: same as `for x in self`
5. `__reversed__`: same as `reversed(self)`

``` py
class MyList:
    def __init__(self, values=None):
        if values is None:
            self.values = []
        else:
            self.values = values

    def __len__(self):
        return len(self.values)

    def __getitem__(self, key):
        return self.values[key]

    def __setitem__(self, key, value):
        self.values[key] = value

    def __iter__(self):
        return iter(self.values)

    def __reversed__(self):
        return reversed(self.values)
```

### Context Manager Magic Method

The class implementation methods we discussed in [Context Manager](context_manager.md) also use two magic methods, `__enter__` and `__exit__`.

``` py
class OpenFile():
    def __init__(self, filename: str, mode: str) -> object:
        self.filename = filename
        self.mode = mode

    def __enter__(self):
        self.file_obj = open(self.filename, self.mode)
        return self.file_obj

    def __exit__(self, except_type, except_val, except_traceback):
        self.file_obj.close()
```

# Related Articles

| Article                          | Link                                                           |
| -------------------------------- | -------------------------------------------------------------- |
| Python中的__init__和__new__      | https://www.zlovezl.cn/articles/__init__-and__new__-in-python/ |
| Python Tutorial: str() vs repr() | https://www.youtube.com/watch?v=5cvM-crlDvg                    |

# Method vs. Classmethod vs. Staticmethod

A class can have three types of methods, a `general method`, a `class method`, and a `static method`.

## Table of Contents

* [Method vs. Classmethod vs. Staticmethod](#method-vs-classmethod-vs-staticmethod)
  * [Table of Contents](#table-of-contents)
  * [Method](#method)
  * [Classmethod](#classmethod)
    * [Usage 1: Modify Class Variables](#usage-1-modify-class-variables)
    * [Usage 2: Alternative Class Constructor](#usage-2-alternative-class-constructor)
  * [Staticmethod](#staticmethod)

## Method

General methods are those `instance methods` where the first receive argument must be `self`.

``` py
class Person:
    def __init__(self, name):
        self.name = name

    def hi(self):
        print(self.name)


x = Person("Jay")
x.hi()        # Jay
Person.hi(x)  # Jay
```

## Classmethod

`Class method`, on the other hand, is a method exclusive to class, so the first argument it receives is no longer `self` (instance itself) but `cls` (**class itself**).

But remember to add the [**@classmethod** decorator](../assets/must_know/closure_decorator.png) to the `class method`'s head so that python recognizes that the first argument is the class itself and not the instance.

### Usage 1: Modify Class Variables

The first use of `class method` is to modify class variables.

``` py
class Person:
    count = 0

    @classmethod
    def changeCount(cls, newCount):
        cls.count = newCount


x = Person()

Person.changeCount(10)
print(Person.count)  # 10
print(x.count)       # 10
```

### Usage 2: Alternative Class Constructor

The second use of `class method` is to use it as an additional class constructor, e.g. to quickly convert a string to a class without sacrificing design.

``` py
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def fromString(cls, cls_str):
        return cls(*cls_str.split("-"))


person_str1 = "Jay-24"
person1 = Person.fromString(person_str1)
print(person1.name)  # Jay 
print(person1.age)   # 24
```

## Staticmethod

The `static method` is used when you will not use instance `self` or class `cls`, but the logic of the method is very relevant to class.

``` py
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @staticmethod
    def splitPersonString(string, split_sign="-"):
        return string.split(split_sign)

    @classmethod
    def fromString(cls, cls_str):
        return cls(*cls.splitPersonString(cls_str, ","))


person_str1 = "Jay,24"
person1 = Person.fromString(person_str1)
```

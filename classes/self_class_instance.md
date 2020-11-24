# self (class instance)

When implementing the `class`, regardless of whether it is `__init__` or any other method, you can often see `self` appear in the parameter. What exactly is `self`?

## Table of Contents

* [self (class instance)](#self-class-instance)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)

## Basic

Simply put, `self` stands for the "object" who was created to take advantage of this `class`, the `instance` itself.

``` py
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
        print(self)   # <__main__.Person object at 0x000001F5DBCB8708>


p = Person("Jay", 20)
print(p)              # <__main__.Person object at 0x000001F5DBCB8708>
```

So when your class has a function with an instance, you can use a function with class and pass an instance into it.

``` py
class Person:
    def say(self):
        print('Hello')


p = Person()
Person.say(p)  # Exactly the same as `p.say()`
```

There is no meaning, but python accepts it.

<!-- TODO: See if it is related to class method -->
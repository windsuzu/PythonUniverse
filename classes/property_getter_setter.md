# @Property (Getter, Setter)

In a previous post [_ (private) vs. __ (name mangling)](classes/private_name_mangling.md), we covered python's implementation of methods similar to "private" in Java. In this post, we will use python to implement `getter` & `setter` similar to Java.

## Table of Contents

* [@Property (Getter, Setter)](#property-getter-setter)
  * [Table of Contents](#table-of-contents)
  * [Emulation of Java](#emulation-of-java)
  * [@Property](#property)
  * [Usage 1: Password Accessibility](#usage-1-password-accessibility)
  * [Usage 2: Variable Observer](#usage-2-variable-observer)
* [Related Articles](#related-articles)

## Emulation of Java

For example, we want to use `setter` and `getter` to access the cat's name.

``` py
class Cat:
    def __init__(self, name):
        self._name = name

    def getName(self):
        return self._name

    def setName(self, new_name):
        self._name = new_name


cat = Cat("mimi")
cat.setName("dada")
print(cat.getName())  # dada
```

Seems perfect, but python provides `@property` to achieve a more pythonic approach! 

## @Property

`@property` is a [decorator](../must_know/closure_decorator.md) that returns results in real time based on class variables, but it cannot be modified at this time. If you want to change the property (and variables with the property), then use `@variable_name.setter`.

``` py
class Cat:
    def __init__(self, name):
        self.name = name  # <-------- 1

    @property
    def name(self):
        print("getter triggered")
        return self._name

    @name.setter
    def name(self, new_name):  # <--- 2
        print("setter triggered")
        self._name = new_name


cat = Cat("mimi")  # setter triggered

cat.name = "dada"  # setter triggered
print(cat.name)    # getter triggered
                   # dada
```

In the above example, the `self.name` in `__init__` is actually a call to `@name.setter`, which stores the `name` into the private variable `_name`. Then if an instance calls `.name`, then the private variable `_name` is actually retrieved from property `name()`.


## Usage 1: Password Accessibility

The first example of using `@property` is to enhance password security.

When creating the User `instance`, the given password goes into the `setter` to generate an encrypted hash password, and then store it into `password_hash`. Now you can't get the password with `user_instance.password`.

To authenticate that the password is correct, use the new function `verify_password` to verify that the input password hash is the same as `password_hash`.

``` py
class User:
    def __init__(self, password):
        self.password = password 

    @property
    def password(self):
        raise AttributeError("password is not readable.")

    @password.setter
    def password(self, password):
        self.password_hash = generate_password_hash(password)

    def verify_password(self, password):
        return check_password_hash(self.password_hash, password)
```

## Usage 2: Variable Observer

The second use of `@property` is to access variables in an observer-like manner.

For example, below, the `fullname` property will be changed along with the `first_name` and `last_name` of the class. We can also use `fullname.setter` to change the `first_name` and `last_name` of a fullname.

``` py
class User:
    def __init__(self, first_name, last_name):
        self.first_name = first_name
        self.last_name = last_name

    @property
    def fullname(self):
        return f"{self.first_name} {self.last_name}"

    @fullname.setter
    def fullname(self, fullname):
        self.first_name, self.last_name = fullname.split(" ")


user = User("Mimi", "Wang")
print(user.fullname)         # Mimi Wang
user.first_name = "Sansan"
print(user.fullname)         # Sansan Wang

user.fullname = "Dada Wang"
print(user.fullname)         # Dada Wang
print(user.first_name)       # Dada
```

# Related Articles

| Article                                                                     | Link                                                                         |
| --------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| [Python] setter 和 getter                                                   | https://medium.com/bryanyang0528/python-setter-%E5%92%8C-getter-6c08a9d37d46 |
| [Python教學]@property是什麼? 使用場景和用法介紹                             | https://www.maxlist.xyz/2019/12/25/python-property/                          |
| Python OOP Tutorial 6: Property Decorators - Getters, Setters, and Deleters | https://www.youtube.com/watch?v=jCzT9XFZ5bw                                  |
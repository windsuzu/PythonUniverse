# Variables (class & instance)

There are two types of variables in the class, one are `class variables`, and the other are `instance variables`.

## Table of Contents

* [Variables (class & instance)](#variables-class--instance)
  * [Table of Contents](#table-of-contents)
  * [Class Variables](#class-variables)
  * [Instance Variables](#instance-variables)
  * [Combined (class & instance)](#combined-class--instance)

## Class Variables

The `class variables` will always stick to the `class`, and can be called by `instance`. One use is as a `counter`.

``` py
class Employee:
    num_emp = 0

    def __init__(self):
        Employee.num_emp += 1  # <----- Calling variables with class is class variable.
        

e1 = Employee()
e2 = Employee()
print(Employee.num_emp)  # 2
print(e1.num_emp)        # 2
print(e2.num_emp)        # 2
```

We can also use `instance` to get the class variable.

## Instance Variables

An `instance variable` exists only on an `instance`.

``` py
class Employee:
    def __init__(self, pay):
        self.pay = pay


e1 = Employee(10000)
e2 = Employee(20000)
print(Employee.pay)  # AttributeError: type object 'Employee' has no attribute 'pay'
print(e1.pay)        # 10000
print(e2.pay)        # 20000
```

## Combined (class & instance)

A variable can be both a `class variable` and an `instance variable`, although this should not be done in general.

``` py
class Employee:
    count = 0

    def __init__(self):
        Employee.count += 1
        self.count += 1


e1 = Employee()
e2 = Employee()

print(Employee.count)  # 2
print(e1.count)        # 2
print(e2.count)        # 3
```

Now you should be able to see the reason for the value of these variables.

1. `Employee.count` is a **class variable**, no problem.
2. `e1.count` is an **instance variable** which, when created, is created by taking the class variable `Employee.count (1) + 1 = 2`.
3. `e2.count` is also an **instance variable** which is created by taking the class variable `Employee.count (2) + 1 = 3`.

In the above example, instance and class variable are completely separated, so the changes do not affect each other.

``` py
e1.count = 0
print(Employee.count)  # 2
print(e1.count)        # 0
print(e2.count)        # 3

Employee.count = 0
print(Employee.count)  # 0
print(e1.count)        # 0
print(e2.count)        # 3
```

This is because the instance will first go to its own `__dict__` to see if any variables match, and then to the class's `__dict__` if there are none. 

Now, if only the class variable exists in an instance, then when the class variable is modified, the variables called from the instance will be modified as well.

``` py
class Employee:
    count = 0

    def __init__(self):
        Employee.count += 1


e1 = Employee()
Employee.count = 0
print(Employee.count)  # 0
print(e1.count)        # 0
```
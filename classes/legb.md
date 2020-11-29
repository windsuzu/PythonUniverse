# LEGB (local, enclosing, global, builtins)

According to python documentation: [9.2. Python Scopes and Namespaces](https://docs.python.org/3/tutorial/classes.html#python-scopes-and-namespaces), when a variable is called, the system will follow the `LEGB rules` to lookup the table with the corresponding scope and then return the value.

## Table of Contents

* [LEGB (local, enclosing, global, builtins)](#legb-local-enclosing-global-builtins)
  * [Table of Contents](#table-of-contents)
  * [Overview of LEGB](#overview-of-legb)
  * [Global x](#global-x)
  * [Nonlocal x](#nonlocal-x)
  * [Scopes and Namespaces Example](#scopes-and-namespaces-example)
* [Related Articles](#related-articles)

## Overview of LEGB

Here is an example to see LEGB four scopes at once.

When we use the `min` in `inner()`, system first check if it exists in `local`, if not, then check if it exists in `enclosing`, then `global`, then `builtins`.

Since a `min` exists in `local`, it returns `"local min"`.

``` py
from builtins import min

min([1, 2, 3])  # <------------- builtins
min = "global min"  # <--------- global

def outer():
    min = "enclosing min"  # <-- enclosing

    def inner():
        min = "local min"  # <-- local
```

## Global x

In general, we cannot modify the `global` variables when we are `local`. This behavior will cause `UnboundLocalError`, because `local` will mistakenly think that it is handling an **undefined local variable**.

``` py
a = 1

def func():
    a = a + 1  # UnboundLocalError: local variable 'a' referenced before assignment
```

Let's examine what happens inside `func()`. Actually, there is no problem with `a=`; the problem is with `a + 1`. The first `a` is trying to define a local variable, but the last `a` wants to use it before it is defined.

But all you want to do is modify the **global** `a`. so python provides a `global` syntax that allows you to modify the **global** `a`.

``` py
a = 1

def func():
    global a  # I want to modify global a !!
    a = a + 1

func()
print(a)      # 2
```

## Nonlocal x

The same occurs in the **nested scope** (which defines function inside function).

``` py
def outer():
    a = 1

    def inner():
        a += 1  # UnboundLocalError: local variable 'a' referenced before assignment

    inner()
    print(a)
```

It's just that this time we want to change the `a` inside the enclosing function. (⁂ for the enclosing function `outer`, `a` is its **local variable!**)

``` py
def outer():
    a = 1

    def inner():
        nonlocal a  # I want to modify enclosing function's a !!
        a += 1  

    inner()
    print(a)        # 2

outer()
```

## Scopes and Namespaces Example

With all the above knowledge, you can now challenge the [9.2. Python Scopes and Namespaces](https://docs.python.org/3/tutorial/classes.html#python-scopes-and-namespaces) example!

``` py
def scope_test():
    def do_local():
        spam = "local spam"

    def do_nonlocal():
        nonlocal spam
        spam = "nonlocal spam"

    def do_global():
        global spam
        spam = "global spam"

    spam = "test spam"
    do_local()
    print("After local assignment:", spam)
    do_nonlocal()
    print("After nonlocal assignment:", spam)
    do_global()
    print("After global assignment:", spam)

scope_test()
print("In global scope:", spam)
```

The output of the example code is:

```
After local assignment: test spam
After nonlocal assignment: nonlocal spam
After global assignment: nonlocal spam
In global scope: global spam
```

If there is a question, it should be why `After global assignment: nonlocal spam` and not `After global assignment: global spam`! This is because when you run `print("After global assignment:", spam)`, it's still in `scope_test()`.


# Related Articles

| Article             | Link                                                                        |
| ------------------- | --------------------------------------------------------------------------- |
| 聊聊 Python Closure | https://medium.com/@dboyliao/%E8%81%8A%E8%81%8A-python-closure-ebd63ff0146f |
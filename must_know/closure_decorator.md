# Decorator

<!-- TODO: Links to articles on property, classmethod, etc. -->
Decorator will be seen in many places, such as [@property](), [@classmethod](), [@staticmethod](), and so on.

Generally, the developer wants to implement decorator in order to achieve the effect of logger or timer.

## Table of Contents

* [Decorator](#decorator)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
    * [Closure](#closure)
    * [Decorator](#decorator-1)
    * [Original Functions with parameters](#original-functions-with-parameters)
    * [Original Functions with returns](#original-functions-with-returns)
  * [Decorator Class](#decorator-class)
  * [Multiple Decorators](#multiple-decorators)
  * [Decorators With Arguments](#decorators-with-arguments)
* [Related Articles](#related-articles)

## Basic

### Closure

Decorator is actually an implementation of closure, here is an example of closure.

We define an `outer function` and an `inner function` inside it. This `inner function` will print out the arguments `msg` passed in the `outer function`. Then, at the end of the `outer function`, return this defined `inner function`.

And then we implement two objects: `str_func` and `int_func` which are the `inner_function` waiting to be executed, and both hold the `msg` from the argument of the `outer_function`.

``` py
def outer(msg):
    def inner():
        print(msg)
    return inner

str_func = outer("Hi")
int_func = outer(100)

str_func()  # Hi
int_func()  # 100
```

This `outer` returns an `inner` that is waiting to be executed, which is a **closure**.

### Decorator

Decorator just replaces the `msg` part with a function `orig_func` to be decorated.

``` py
def decorator(orig_func):
    def wrapper():
        print(f"func name: {orig_func.__name__}")
        orig_func()

    return wrapper
```

In the above decorator, we will decorate any function to be executed, and then it will print out the name of the function every time we run it. We have two ways to decorate `orig_func`.

The first one is to pass `orig_func` into `decorator` in the usual way, as an argument.

``` py
def greet():
    print("Hello")

func1 = decorator(greet)
func1()
# func name: greet
# Hello
```

The second is to add the annotation of `decorator` over the `orig_func` function.

``` py
@decorator
def greet():
    print("Hello")

greet()
# func name: greet
# Hello
```

### Original Functions with parameters

What if `orig_func` has parameters? This is where the [*args \& **kwarg](args_kwargs.md) trick comes in!

All we need to do is add `*args & **kwarg` into `wrapper` and enter them into `orig_func`.

``` py
def decorator(orig_func):
    def wrapper(*args, **kwargs):
        print(f"func name: {orig_func.__name__}")
        print(f"func args: {args}, {kwargs}")
        orig_func(*args, **kwargs)

    return wrapper

@decorator
def greet(msg, name="User"):
    print(f"{msg}! {name}!")


greet("Hello", name="Jay")
# func name: greet
# func args: ('hello',), {'name': 'Jay'}
# Hello! Jay!
```

### Original Functions with returns

If we want to change `orig_func` above so that it returns the greeting string, then we will get `None`, to solve this problem just make the wrapper of the decorator return `orig_func`.

``` py
def decorator(orig_func):
    def wrapper(*args, **kwargs):
        print(f"func name: {orig_func.__name__}")
        print(f"func args: {args}, {kwargs}")
        func = orig_func(*args, **kwargs)
        return func

    return wrapper

@decorator
def greet(msg, name="User"):
    return f"{msg}! {name}!"


msg = greet("Hello", name="Jay")
# func name: greet
# func args: ('Hello',), {'name': 'Jay'}

print(msg)
# Hello! Jay!
```

## Decorator Class

Another way to implement a decorator is through classes, but this is less commonly used. The following `decorator_class` example would have the exact same effect as the `function` version above.

``` py
class decorator:
    def __init__(self, orig_func):
        self.orig_func = orig_func

    def __call__(self, *args, **kwargs):
        print(f"func name: {self.orig_func.__name__}")
        print(f"func args: {args}, {kwargs}")
        self.orig_func(*args, **kwargs)
```

## Multiple Decorators

Order is important when there are multiple decorators decorating an `orig_func` at the same time, and there may be some unexpected problems. For example, in the following example, `logger` is printing the name of `timer.wrapper` instead of `orig_func`.

``` py
def logger(orig_func):
    def wrapper(*args, **kwargs):
        print(f"func name: {orig_func.__name__}")
        orig_func(*args, **kwargs)

    return wrapper


def timer(orig_func):
    import time

    def wrapper(*args, **kwargs):
        t1 = time.time()
        orig_func(*args, **kwargs)
        t2 = time.time() - t1
        print(f"func [{orig_func.__name__}] exec time: {t2}")

    return wrapper


@logger
@timer
def greet(msg):
    print(msg)


greet("hello")
# func name: wrapper
# hello
# func [greet] exec time: 0.001
```

If you don't like the result, and you want `logger` to print the name of `orig_func` as well, then you can use `functools.wraps` to solve the problem.

Simply put the `wraps(orig_func)` annotation on the `wrapper`'s head in the decorator where the `orig_func` is replaced by the `wrapper` and you're good to go!

``` py
from functools import wraps

def timer(orig_func):
    import time

    @wraps(orig_func)  # <--------------- Solved
    def wrapper(*args, **kwargs):
        ...
        ...

    return wrapper


@logger
@timer
def greet(msg):
    print(msg)


greet("hello")
# func name: greet
# hello
# func [greet] exec time: 0.001
```

## Decorators With Arguments

Now you may have a requirement, you need to add parameters to the decorator. This may seem haphazard, but here is an example of how to do it.

``` py
def decorator(orig_func):
    def wrapper(*args, **kwargs):
        print(f"func name: {orig_func.__name__}")
        print(f"func args: {args}, {kwargs}")
        orig_func(*args, **kwargs)

    return wrapper
```

We want to add a number `count` to the original decorator that represents how many times we want to run `orig_func`.

``` py
def count_decorator(count):  # <------------------------ new decorator with argument 
    def decorator(orig_func):
        def wrapper(*args, **kwargs):
            print(f"func name: {orig_func.__name__}")
            print(f"func args: {args}, {kwargs}")

            for _ in range(count):  # <----------------- use the argument
                orig_func(*args, **kwargs)

        return wrapper
    return decorator  # <------------------------------- return the original decorator
```

We add a `count_decorator(count)` to the outermost layer and return the original decorator as well. Now we can use `count_decorator` as a decorator with parameters.

``` py
@count_decorator(2)
def greet(msg):
    print(msg)

greet("hello")
# func name: greet
# func args: ('hello',), {}
# hello
# hello
```

# Related Articles

| Articles                                                                            | Link                                        |
| ----------------------------------------------------------------------------------- | ------------------------------------------- |
| What Does It Take To Be An Expert At Python?                                        | https://www.youtube.com/watch?v=7lmCu8wz8ro |
| Python Tutorial: Decorators - Dynamically Alter The Functionality Of Your Functions | https://www.youtube.com/watch?v=FsAPt_9Bf3U |
| Python Tutorial: Decorators With Arguments                                          | https://www.youtube.com/watch?v=KlBPCzcQNU8 |

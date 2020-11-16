# *args and **kwargs

When you have more than one but are not sure how many parameters you want to throw into a function, you can use the `*args `and `**kwargs` tricks to implement them.

## Table of Contents

* [*args and **kwargs](#args-and-kwargs)
  * [Table of Contents](#table-of-contents)
  * [*args](#args)
  * [**kwargs](#kwargs)
  * [Combination of *arg and **kwargs](#combination-of-arg-and-kwargs)
* [Related Articles](#related-articles)

## *args

The `*args` will be a tuple format in the function. Because the `*` syntax is a method used to collect things into a tuple.

For example, the built-in `sum()` only takes a iterable, so we can change it to parameter mode.

``` py
def my_sum(*arg):
    print(type(arg))  # tuple
    return sum(arg)

sum([1, 2, 3, 4, 5])   # 15
my_sum(1, 2, 3, 4, 5)  # 15
```

## **kwargs

The `**kwargs` will be a dict format in the function. Because the `**` syntax is a method used to collect things into a dict.

We can also use the dict function `setdefault()` to define the default incoming parameters.

``` py
def greet(msg, **kwarg):
    print(type(kwarg))  # dict
    kwarg.setdefault('name', 'User')
    print(f"{msg}! {kwarg['name']}!")


greet('Hello')  # Hello! User!
greet('Hello', name="Jay")  # Hello! Jay!
```

## Combination of *arg and **kwargs

`*arg` and `**kwarg` can be used together. General parameters can also be used together with `*arg` and `**kwarg`.

``` py
def example(a, *arg, b=0, **kwarg):
    print(a)     # 1
    print(arg)   # (2, 3)
    print(b)     # 1
    print(kwarg) # {'x': 'a', 'y': [1, 2, 3]}

example(1, 2, 3, b=1, x='a', y=[1, 2, 3])
```

Arguments after `*arg` will become **keyword arguments** (`b` in the example above). Be sure to assign a value to them, or define an initial value for them.

# Related Articles

| Article                                           | Link                                                              |
| ------------------------------------------------- | ----------------------------------------------------------------- |
| [Python] *args 和 **kwargs 是什麼？一次搞懂它們！ | https://skylinelimit.blogspot.com/2018/04/python-args-kwargs.html |
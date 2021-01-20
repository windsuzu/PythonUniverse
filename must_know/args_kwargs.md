# *args and **kwargs

When you have more than one but are not sure how many parameters you want to throw into a function, you can use the `*args `and `**kwargs` tricks to implement them.

## Table of Contents

* [*args and **kwargs](#args-and-kwargs)
  * [Table of Contents](#table-of-contents)
  * [*args](#args)
  * [**kwargs](#kwargs)
  * [Defining Functions with *arg and **kwarg](#defining-functions-with-arg-and-kwarg)
  * [Calling Functions with *arg and **kwarg](#calling-functions-with-arg-and-kwarg)
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

## Defining Functions with *arg and **kwarg

We can use `*arg` and `**kwarg` together, and they can also cooperate with general parameters.

``` py
def example(a, *arg, b=0, **kwarg):
    print(a)     # 1
    print(arg)   # (2, 3)
    print(b)     # 1
    print(kwarg) # {'x': 'a', 'y': [1, 2, 3]}

example(1, 2, 3, b=1, x='a', y=[1, 2, 3])
```

The arguments after `*arg` will be identified as the **keyword arguments** (e.g., `b` in the example above), and you should remember to assign a value to them, or define an initial value for them.

## Calling Functions with *arg and **kwarg

`tuple` and `list` can be extracted as the arguments (`*arg`), and `dict` can be extracted as the keyword arguments (`**kwarg`).

``` py
def func(greet, time, name):
    print(greet, time, name)


func(*["Good", "Morning"], **{"name": "Maria"})
# Good Morning Maria
```

In the above example, the `Good` and `Morning` from the first list are extracted and pass to the `func` as the arguments (`greet` and `time`), and the `Maria` is treated as the keyword argument (`name`) and pass to the `func`.

# Related Articles

| Article                                           | Link                                                                   |
| ------------------------------------------------- | ---------------------------------------------------------------------- |
| [Python] *args 和 **kwargs 是什麼？一次搞懂它們！ | https://skylinelimit.blogspot.com/2018/04/python-args-kwargs.html      |
| Unpacking in Python: Beyond Parallel Assignment   | https://stackabuse.com/unpacking-in-python-beyond-parallel-assignment/ |
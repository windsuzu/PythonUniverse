# Defaultdict

`defaultdict` has all the functions of a `dict`, to be precise, it is a subclass of `dict`. except that it does not raise `KeyError` but returns a default value.

## Table of Contents

* [Defaultdict](#defaultdict)
  * [Table of Contents](#table-of-contents)
  * [Bad way to handle KeyError](#bad-way-to-handle-keyerror)
  * [Better way to handle KeyError](#better-way-to-handle-keyerror)
  * [Best: Defaultdict](#best-defaultdict)
    * [Default Factory](#default-factory)
      * [Default Factory with Function and Lambda](#default-factory-with-function-and-lambda)
      * [Default Factory with Int](#default-factory-with-int)
      * [Default Factory with List](#default-factory-with-list)
* [Related Articles](#related-articles)


## Bad way to handle KeyError

When we use dict, we can first make sure that the key is in the `dict`, and then take it out.

``` py
d = {"val": 10, "val2": 20}

if "val" in d:
    print(d["val"])
else:
    d["val"] = 10
    print(d["val"])
```

## Better way to handle KeyError

We can use `dict`'s built-in function `get()` to get the value and define a default value to prevent the `KeyError`.

``` py
d = {"val": 10, "val2": 20}
d.get("val", 10)  # Instead of d["val"]
```

## Best: Defaultdict

The first parameter of the `defaultdict` must be the default value (factory). After that, we can put the initial `dict` object into the parameters.

``` py
from collections import defaultdict

d = defaultdict(lambda: -1, {"val": 10, "val2": 20})

d["val"]   # 10
d["val3"]  # -1
d          # defaultdict(<function __main__.<lambda>()>,
           #         {'val': 10, 'val2': 20, 'val3': -1})
```

### Default Factory

Default factory must be a function to determine the default value of the corresponding key when the `KeyError` occurred.

#### Default Factory with Function and Lambda

``` py
def def_value(): 
    return "No value"

d = defaultdict(def_value) 

# same as

d = defaultdict(lambda: "No value")

d["a"] = 1
d["b"]

d  # {'a': 1, 'b': 'No value'}
```

#### Default Factory with Int

When the `int` class is passed as the `default_factory`, then a `defaultdict` is created with the default value as `0`.

``` py
d = defaultdict(int)
d["a"] = 1
d["b"]

d  # {'a': 1, 'b': 0}
```

#### Default Factory with List

When the `list` class is passed as the `default_factory`, then a `defaultdict` is created with the values that are `list`.

``` py
d = defaultdict(list)
d["a"] = [1, 2, 3]
d["b"].append(4)
d["c"].extend([5, 6])

d  # {'a': [1, 2, 3], 'b': [4], 'c': [5, 6]}
```

# Related Articles

| Article                                   | Link                                                 |
| ----------------------------------------- | ---------------------------------------------------- |
| 7 More Tricks to Write Better Python Code | https://www.youtube.com/watch?list=LL&t=1319         |
| Defaultdict in Python                     | https://www.geeksforgeeks.org/defaultdict-in-python/ |
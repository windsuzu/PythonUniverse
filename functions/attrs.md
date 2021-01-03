# hasattr, getattr, setattr, delattr

These are the four built-in python methods for quickly accessing the attributes (properties) of object instances.

# Table of Contents

* [hasattr, getattr, setattr, delattr](#hasattr-getattr-setattr-delattr)
* [Table of Contents](#table-of-contents)
  * [Basic](#basic)
  * [Usage](#usage)
* [Related Articles](#related-articles)

## Basic

| Function | Parameter                        | Description                                                                           |
| -------- | -------------------------------- | ------------------------------------------------------------------------------------- |
| hasattr  | (object, attr_name)              | Returns a `bool` to tell you if the object has the attribute.                         |
| getattr  | (object, attr_name, default_val) | Returns the value of the object attribute, or the default value if it does not exist. |
| setattr  | (object, attr_name, val)         | Set the value of the object attribute. Same as `object.attr_name = val`               |
| delattr  | (object, attr_name)              | Delete the attribute of the object. Same as `del object.attr_name`                    |

``` py
class Cat:
    def __init__(self):
        self.age = 0


cat = Cat()
hasattr(cat, "age")  # True
setattr(cat, "age", 10)
getattr(cat, "age", -1)  # 10
delattr(cat, "age")
getattr(cat, "age", -1)  # -1
cat.age  # # AttributeError: 'Cat' object has no attribute 'age'
```

## Usage

This can be useful when you use list of dict to declare many instances.

``` py
class Cat:
    ...

listOfCats = []
attrs = [{"name": "meow1", "age": 5}, {"name": "meow2", "age": 10}]

for attr in attrs:
    cat = Cat()
    for key, val in attr.items():
        setattr(cat, key, val)
    listOfCats.append(cat)

cat1, cat2 = listOfCats
cat1.name  # meow1 
cat1.age   # 5
cat2.name  # meow2
cat2.age   # 10
```

# Related Articles

| Article                                            | Link                                                                                        |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| Using getattr, setattr, delattr, hasattr in Python | https://medium.com/@pranaygore/using-getattr-setattr-delattr-hasattr-in-python-6d79c6f9fda3 |
| Why use setattr() and getattr() built-ins?         | https://stackoverflow.com/questions/19123707/why-use-setattr-and-getattr-built-ins          |
| 10 Python Tips and Tricks For Writing Better Code  | https://youtu.be/C-gEQdGVXbk?t=1511                                                         |
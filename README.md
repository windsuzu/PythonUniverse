![](assets/python_universe.gif)

In this Python Universe, I want to learn and show you all the Python skills.

All skills are base on the implementation of Python 3.

# Table of contents

<!-- \[(.*)\]\((.*)\) -->
<!-- <li><a href="$2">$1</li> -->

<table>
<tr><th>Must Know</th><th>Classes</th><th>Functions</th></tr>
<tr>
<td>
<ul style="margin: 8px">
<li><a href="#list--dict--set-comprehensions">List & Dict & Set Comprehensions</li>
<li><a href="#lambda-functions">Lambda Functions</li>
<li><a href="#map">Map</li>
<li><a href="#filter">Filter</li>
<li><a href="#zip">Zip</li>
<li><a href="#reduce">Reduce</li>
<li><a href="#args--kwargs">*args & **kwargs</li>
<li><a href="#generator-map-filter-zip">Generator (map, filter, zip)</li>
<li><a href="#closure--decorator">Closure & Decorator</li>
<li><a href="#context-manager">Context Manager</li>
<li><a href="#magic-method">Magic Method</li>
<li><a href="#metaclasses">Metaclasses</li>
<li><a href="#threading--multiprocessing">Threading & Multiprocessing</li>
</ul>
</td>

<td>
<ul style="margin: 8px">
<li><a href="#self-class-instance">self (class instance)</li>
<li><a href="#variables-class--instance">variables (class & instance)</li>
<li><a href="#method-vs-classmethod-vs-staticmethod">method vs. classmethod vs. staticmethod</li>
<li><a href="#\_-private-vs-\__-name-mangling">_ (private) vs. __ (name mangling)</li>
<li><a href="#property-getter-setter">@property (getter, setter)</li>
<li><a href="#legb-local-enclosing-global-builtins">LEGB (local, enclosing, global, builtins)</li>
<li><a href="#abstract-class">Abstract class</li>
<li><a href="#dataclasses">Dataclasses</li>
<li><a href="#classes-in-dynamic-language">Classes in Dynamic Language</li>
</ul>
</td>

<td>
<ul style="margin: 8px">
<li><a href="#enclosing-function">Enclosing function</li>
<li><a href="#attrs">Attrs</li>
<li><a href="#functions-in-dynamic-language">Functions in Dynamic Language</li>
</ul>
</td>

</tr>
</table>

<table>
<tr><th>Collections</th><th>Itertools</th></tr>
<tr>
<td rowspan="3">
<ul style="margin: 8px">
<li><a href="#defaultdict">defaultdict</li>
<li><a href="#ordereddict">OrderedDict</li>
<li><a href="#counter">Counter</li>
<li><a href="#namedtuple">namedtuple</li>
<li><a href="#deque">deque</li>
</ul>

<td>
<ul>
<li><a href="#count">count</li>
<li><a href="#cycle">cycle</li>
<li><a href="#repeat">repeat</li>
</ul>
</td>
<tr><td>
<ul>
<li><a href="#accumulate">accumulate</li>
<li><a href="#chain">chain</li>
<li><a href="#compress">compress</li>
<li><a href="#filterfalse">filterfalse</li>
<li><a href="#groupby">groupby</li>
<li><a href="#islice">islice</li>
<li><a href="#starmap">starmap</li>
<li><a href="#takewhile">takewhile</li>
<li><a href="#dropwhile">dropwhile</li>
<li><a href="#zip_longest">zip_longest</li>
</ul>
</td></tr>
<tr><td>
<ul>
<li><a href="#product">product</li>
<li><a href="#permutations">permutations</li>
<li><a href="#combinations">combinations</li>
</ul>
</td></tr>
</tr>
</table>

# Must Know

## [List & Dict & Set Comprehensions](must_know/list_dict_set_comprehensions.md)

``` py
[(i, j) for i in range(3) for j in range(3) if i > j]

# [(1, 0), (2, 0), (2, 1)]
```

## [Lambda Functions](must_know/lambda_functions.md)

``` py
li = [1, 2, 3]
li = [*map(lambda x: x * 10, li)]

#li = [10, 20, 30]
```

## [Map](must_know/map.md)

``` py
num1 = [100, 1, 20]
num2 = [19, 4, 94]
num3 = [40, 6, 30]

[*map(lambda x, y, z: max(x, y, z), num1, num2, num3)]
# [100, 6, 94]
```

## [Filter](must_know/filter.md)

``` py
names = ['Liam', 'Olivia', 'Noah', 'Emma', 'Oliver', 'Ava']
choice = filter(lambda x: x.startswith('O'), names)

print(*choice, sep=', ') # Olivia, Oliver
```

## [Zip](must_know/zip.md)

``` py
a = [1, 2, 3]
b = [4, 5, 6]

c = [*zip(a, b)]  # [(1, 4), (2, 5), (3, 6)]
a, b = zip(*c)    # a=(1, 2, 3),  b=(4, 5, 6)
```

## [Reduce](must_know/reduce.md)

``` py
from functools import reduce
reduce(lambda x, y: x - y, [1, 2, 3, 4, 5], 100)  # 85
```

## [*args & **kwargs](must_know/arg_kwarg.md)

``` py
def example(a, *arg, b=0, **kwarg):
    print(a)     # 1
    print(arg)   # (2, 3)
    print(b)     # 1
    print(kwarg) # {'x': 'a', 'y': [1, 2, 3]}

example(1, 2, 3, b=1, x='a', y=[1, 2, 3])
```

## [Generator (map, filter, zip)](must_know/generator.md)

``` py
def square_it(value):
    for i in range(value):
        yield i**2

li = square_it(10_000_000)

[i for i in li if i < 50]  # [0, 1, 4, 9, 16, 25, 36, 49]
```

## [Closure & Decorator](must_know/closure_decorator.md)

``` py
def count_decorator(count):  # new decorator with argument
    def decorator(orig_func):
        def wrapper(*args, **kwargs):
            print(f"func name: {orig_func.__name__}")
            print(f"func args: {args}, {kwargs}")

            for _ in range(count):  # use the argument
                orig_func(*args, **kwargs)

        return wrapper
    return decorator  # return the original decorator

@count_decorator(2)
def greet(msg):
    print(msg)


greet("hello")
# func name: greet
# func args: ('hello',), {}
# hello
# hello
```

## [Context Manager](must_know/context_manager.md)

``` py
@contextmanager
def enterFolder(folderName):
    home = os.getcwd()
    os.chdir(folderName)
    yield
    os.chdir(home)

with enterFolder('folder1'), open('example1.txt', 'w') as f:
    f.write('file1')
```

## [Magic Method](must_know/magic_method.md)

``` py
class BinaryInt(str):
    def __new__(cls, val):
        return str.__new__(cls, f"{val: b}")

    def __add__(self, val):
        val += int(self, 2)
        return f"{val:b}"


a = BinaryInt(2)
print(a)      # 10
print(a + 4)  # 110
```

## [Metaclasses](must_know/metaclasses.md)

``` py
class Meta(type):
    def __new__(mtcls, name, bases, attrs):
        if name != "Base" and "must_to_do" not in attrs:
            raise TypeError("Bad Class: must_to_do() is needed")
        return super().__new__(mtcls, name, bases, attrs)


class Base(metaclass=Meta):
    def server_func(self):
        return self.must_to_do()


class Derived(Base):
    ...
# TypeError: Bad Class: must_to_do() is needed
```

## [Threading & Multiprocessing](must_know/threading_multiprocessing.md)

``` py
import concurrent.futures

with concurrent.futures.ThreadPoolExecutor(max_workers=5) as executor:
    futures = [executor.submit(load_url, url, 60) for url in URLS]
    for future in concurrent.futures.as_completed(futures):
        result = future.result()
        print(len(result))


with concurrent.futures.ProcessPoolExecutor() as executor:
    results = executor.map(load_url, URLS, [60] * len(URLS), chunksize=4)
    for result in results:
        print(len(result))
```

# Classes

## [self (class instance)](classes/self_class_instance.md)                  

``` py
class Person:
    def __init__(self, name):
        self.name = name

    def say(self):
        return f"I'm {self.name}"


p = Person("Jay")
p.say() == Person.say(p)  # True
```

## [variables (class & instance)](classes/variables_class_instance.md)       

``` py
class Employee:
    num_emp = 0  # Class variable

    def __init__(self, pay):
        self.pay = pay  # Instance variable
        Employee.num_emp += 1

e1 = Employee(100)
e2 = Employee(200)

e1.num_emp        # 2
Employee.num_emp  # 2

e1.pay  # 100
Employee.pay  # AttributeError: type object 'Employee' has no attribute 'pay'
```

## [method vs. classmethod vs. staticmethod](classes/method_class_static.md) 

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
        return cls(*cls.splitPersonString(cls_str, ", "))


p1 = Person.fromString("Jay, 99")
p1.name  # Jay
p1.age   # 99
```

## [_ (private) vs. __ (name mangling)](classes/private_name_mangling.md)    

``` py
class Dog:
    _weight = 5  # private variable

    def __bark(self):  # name mangling fucntion
        print("bark")


dog = Dog()
dog._weight       # 5
dog.__bark()      # AttributeError: 'Dog' object has no attribute '__bark'
dog._Dog__bark()  # bark
```

## [@property (getter, setter)](classes/property_getter_setter.md)           

``` py
class User:
    def __init__(self, first_name, last_name, password):
        self.first_name = first_name
        self.last_name = last_name
        self.password = password

    @property
    def fullname(self):
        return f"{self.first_name} {self.last_name}"

    @property
    def password(self):
        raise AttributeError("password is not readable.")

    @password.setter
    def password(self, passord):
        from hashlib import md5

        self.password_hash = md5(b"{password}").hexdigest()


user = User("Mimi", "Wang", "0000")
user.fullname       # Mimi Wang
user.password_hash  # 7fbccc9c3a9a5afef65563cd00404c1416
user.password       # Attribute Error: password is not readable.
```

## [LEGB (local, enclosing, global, builtins)](classes/legb.md)              

``` py
min([1, 2, 31])  # builtins min
min = "global min"

def outer():
    # we can do "global min" here to change global
    min = "enclosing min"
    
    def inner():
        # we can do "nonlocal min" here to change enclosing
        min = "local min"
```

## [Abstract class](classes/abstract_class.md)                               

``` py
from abc import ABC, abstractmethod


class Base(ABC, object):
    @property
    @abstractmethod
    def foo(self):
        ...

    @abstractmethod
    def do(self):
        ...
```

## [Dataclasses](classes/dataclasses.md)                                     

``` py
from dataclasses import InitVar, dataclass, field
from typing import List


@dataclass
class InventoryItem:
    name: str
    unit_price: float = field(default=0.0)
    quantity_on_hand: int = field(default=0, repr=False)
    parts: List[str] = field(default_factory=list)
    parts_number: InitVar[int] = 0

    def __post_init__(self, parts_number):
        self.parts.extend([f"part{i}" for i in range(1, parts_number + 1)])


item = InventoryItem("product", parts_number=2)
# InventoryItem (name = 'product', unit_price=0.0, parts=['part1', 'part2'])
```

## [Classes in Dynamic Language](classes/dynamic_language.md)                           

``` py
def getClass(x):
    if x == 1:
        for i in range(11):

            class Example:
                a = i

        return Example


cls = getClass(1)
cls.b = "123"
print(cls.a, cls.b)  # 10 123
```

# Functions

## [Enclosing function](functions/enclosing.md)  

``` py
def add_with_b(b):
    def add(a):
        return a + b
    return add

add4 = add_with_b(4)
add4(3)  # 7
add4(7)  # 11
```

## [Attrs](functions/attrs.md)                       

``` py
class Cat:
    def __repr__(self):
        return f"({self.name}: {self.age})"

listOfCats = []
attrs = [{"name": "meow1", "age": 5}, {"name": "meow2", "age": 10}]

for attr in attrs:
    cat = Cat()
    for key, val in attr.items():
        setattr(cat, key, val)
    listOfCats.append(cat)


print(listOfCats)
# [(meow1: 5), (meow2: 10)]
```

## [Functions in Dynamic Language](functions/dynamic_language.md) 

``` py
for i in range(100):
    def say():
        print(i)


def returnFunc(a):
    if a < 100:
        def mul(b):
            print(a * b)
        return mul
    else:
        def add(b):
            print(a + b)
        return add
```

# Collections

## [defaultdict](collections/defaultdict.md) 

``` py
from collections import defaultdict

d = defaultdict(list)
d["a"] = [1, 2, 3]
d["b"].append(4)
d["c"].extend([5, 6])

# defaultdict(<class 'list'>, {'a': [1, 2, 3], 'b': [4], 'c': [5, 6]})
```

## [OrderedDict](collections/ordereddict.md) 

``` py
from collections import OrderedDict

location = ["C", "B", "A"]
population = [32, 46, 12]

d = OrderedDict({l: p for l, p in zip(location, population)})
# OrderedDict([('C', 32), ('B', 46), ('A', 12)])

d["D"] = 44
# OrderedDict([('C', 32), ('B', 46), ('A', 12), ('D', 44)])

d.popitem(last=False)
# OrderedDict([('B', 46), ('A', 12), ('D', 44)])

d.move_to_end("D", last=False)
# OrderedDict ([( 'D', 44), ('B', 46), ('A', 12)])
```

## [Counter](collections/counter.md)         

``` py
from collections import Counter

c = Counter(cats=4, dogs=8)
# Counter({'dogs': 8, 'cats': 4})

c.update(birds=10)
# Counter({'birds': 10, 'dogs': 8, 'cats': 4})

c = c - Counter({"birds": 5})
# Counter({'dogs': 8, 'birds': 5, 'cats': 4})

c.most_common(2)
# [('dogs', 8), ('birds', 5)]
```

## [namedtuple](collections/namedtuple.md)   

``` py
from collections import namedtuple

Dog = namedtuple("Dog", "name, age")
d1 = Dog("funny", 4)

features = ["happy", 3]
d2 = Dog._make(features)
# Dog(name='happy', age=3)

d2._asdict()
# OrderedDict([('name', 'happy'), ('age', 3)])
```

## [deque](collections/deque.md)             

``` py
from collections import deque

li = [40, 30, 50, 46, 39, 44]
d = deque(li[:2])

# Let 's compute the moving average with range=3
d.appendleft(0)
s = sum(d)

for elem in li[2:]:
    s += elem - d.popleft()
    d.append(elem)
    print(s / 3)
    # 40, 42, 45, 43
```

# Itertools

## [Infinite iterators](itertools/infinite_iterators.md)

### count

``` py
from itertools import count 

gen = count(2.5, 0.5)

for x in gen:
    print(x)
    # 2.5, 3.0, 3.5, 4.0, ... non-stop
```

### cycle

``` py
from itertools import cycle 

gen = cycle([1, 2, 3])

for x in gen:
    print(x)
    # 1, 2, 3, 1, 2, ... non-stop
```

### repeat

``` py
from itertools import repeat 

class Cat:
    ...
    
gen = repeat(Cat(), 2)

for cat in gen:
    print(cat)
    # <__main__.Cat object at 0x0000019AC1C5D348>
    # <__main__.Cat object at 0x0000019AC1C5D348>
```

## [Iterators terminating on the shortest input sequence](itertools/terminated_iterators.md)

### accumulate

``` py
import operator
from itertools import accumulate

gen = accumulate([1, 2, 3, 4])
list(gen)  # [1, 3, 6, 10]


gen = accumulate([1, 2, 3, 4], func=operator.mul)
list(gen)  # [1, 2, 6, 24]
```

### chain

```py
from itertools import chain

gen = chain([1, 2], [3, 4])
list(gen)  # [1, 2, 3, 4]


gen = chain("AB", "CD")
list(gen)  # [A, B, C, D]
```

### compress

```py
from itertools import compress

gen = compress([1, 2, 3], [1, 0, 1])
gen = compress([1, 2, 3], [True, False, True])  # same

list(gen)  # [1, 3]
```

### filterfalse

```py
from itertools import filterfalse

gen = filterfalse(lambda x: x%2 == 0, [1, 2, 3])

list(gen)  # [1, 3]
```

### groupby

```py
from itertools import groupby

gen = groupby("AABBCCCAA")  # default func = lambda x: x
for k, g in gen:
    print(k, list(g))
    # A [A, A]
    # B [B, B]
    # C [C, C, C]
    # A [A, A]


gen = groupby([1, 2, 3, 4], lambda x: x // 3)
for k, g in gen:
    print(k, list(g))
    # 0 [1, 2]
    # 1 [3, 4]


gen = groupby([("A", 100), ("B", 200), ("C", 600)], lambda x: x[1] > 500)
for k, g in gen:
    print(k, list(g))
    # False [(A, 100), (B, 200)]
    # True  [(C, 600)]
```

### islice

```py
gen = islice([1, 2, 3], 2)  # equals to A[:2]
list(gen)  # [1, 2]


gen = islice("ABCD", 2, 4)  # equals to A[2:4]
list(gen)  # [C, D]


gen = islice("ABCD", 0, None, 2)  # equals to A[::2]
list(gen)  # [A, C]
```

### starmap

```py
from itertools import starmap

# with only one argument
gen = starmap(lambda x: x.lower(), "ABCD")
list(gen)  # [a, b, c, d]


# with 2 arguments
gen = starmap(lambda x, y: x + y, [(1, 2), (3, 4)])
list(gen)  # [3, 7]


# with different size of arugments
gen = starmap(lambda *keys: sum(keys) / len(keys), [[3, 8, 3], [4, 2]])
list(gen)  # [4.6666667, 3.0]
```

### takewhile

```py
from itertools import takewhile

gen = takewhile(lambda x: x < 2, [1, 2, 3, 2, 1])
list(gen)  # [1]

gen = takewhile(lambda x: x.isupper(), "ABCdefgHIJ")
list(gen)  # [A, B, C]
```

### dropwhile

```py
gen = dropwhile(lambda x: x < 2, [1, 2, 3, 2, 1])
list(gen)  # [2, 3, 2, 1]


gen = dropwhile(lambda x: x.isupper(), "ABCdefgHIJ")
list(gen)  # [d, e, f, g, H, I, J]
```

### zip_longest

```py
from itertools import zip_longest

gen = zip_longest("ABC", ("X", "Y"))
list(gen)  # [('A', 'X'), ('B', 'Y'), ('C', None)]


gen = zip_longest("ABC", [1, 2], fillvalue=-1)
list(gen)  # [('A', 1), ('B', 2), ('C', -1)]
```

## [Combinatoric iterators](itertools/combinatoric_iterators.md)

### product


```py

```

### permutations


```py

```

### combinations


```py

```

## os

| Tricks  | Simple Demo                                   |
| ------- | --------------------------------------------- |
| pathlib | https://myapollo.com.tw/zh-tw/python-pathlib/ |

## Conditions

| Tricks               | Simple Demo                                                        |
| -------------------- | ------------------------------------------------------------------ |
| Ternary Conditionals | https://www.youtube.com/watch?v=C-gEQdGVXbk&list=LL&index=24&t=34s |

## String

| Tricks  | Simple Demo                                                                                                                              |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| fstring | https://blog.louie.lu/2017/08/08/outdate-python-string-format-and-fstring/, https://www.youtube.com/watch?v=nghuHvKLhJA&list=LL&index=19 |
| getpass | https://www.youtube.com/watch?v=C-gEQdGVXbk&list=LL&index=24&t=1584s                                                                     |

## Int

| Tricks                  | Simple Demo                                                         |
| ----------------------- | ------------------------------------------------------------------- |
| Underscore Placeholders | https://www.youtube.com/watch?v=C-gEQdGVXbk&list=LL&index=24&t=133s |

## List

| Tricks     | Simple Demo                                                                                                     |
| ---------- | --------------------------------------------------------------------------------------------------------------- |
| enumerate  | https://www.youtube.com/watch?v=C-gEQdGVXbk&list=LL&index=24&t=410s, https://youtu.be/VBokjWj_cEA?list=LL&t=189 |
| for...else | https://youtu.be/VBokjWj_cEA?list=LL&t=867                                                                      |

## Set

| Tricks            | Simple Demo                                                                                                    |
| ----------------- | -------------------------------------------------------------------------------------------------------------- |
| set for searching | https://stackoverflow.com/questions/2831212/python-sets-vs-lists/17945009, https://youtu.be/r3R3h5ly_8g?t=1010 |

## Tuple

| Tricks                                                 | Simple Demo                                |
| ------------------------------------------------------ | ------------------------------------------ |
| unpacking https://youtu.be/C-gEQdGVXbk?list=LL&t=1033, | https://youtu.be/SNTZpy0oDB8?list=LL&t=795 |
| swap                                                   | https://youtu.be/VBokjWj_cEA?list=LL&t=445 |
| assign *variable                                       |                                            |

## Dict

| Tricks | Simple Demo                                |
| ------ | ------------------------------------------ |
| get    | https://youtu.be/VBokjWj_cEA?list=LL&t=726 |

## Try

| Tricks | Simple Demo                                 |
| ------ | ------------------------------------------- |
| TEEF   | https://youtu.be/VBokjWj_cEA?list=LL&t=1331 |

## Design

| Tricks      | Simple Demo                                                                                                             |
| ----------- | ----------------------------------------------------------------------------------------------------------------------- |
| annotation  | https://mozillazg.com/2016/01/python-function-argument-type-check-base-on-function-annotations.html                     |
| typing,     | https://myapollo.com.tw/zh-tw/python-typing-module/                                                                     |
| (...), pass | https://stackoverflow.com/questions/42190783/what-does-three-dots-in-python-mean-when-indexing-what-looks-like-a-number |
| absl        | https://www.jianshu.com/p/f84a5b8c1183                                                                                  |

## IPython

| Tricks             | Simple Demo |
| ------------------ | ----------- |
| vscode python file |             |
| timeit, time       |             |
| memit              |             |

## TODOs

| TODOs          |
| -------------- |
| Numba          |
| Numpy          |
| Pandas         |
| Matplotlib     |
| sklearn        |
| pytorch        |
| transformers   |
| tensorboard    |
| mlflow         |
| beautiful soup |
| requests       |
| scrapy         |
| selenium       |
| streamlit      |
| flask          |
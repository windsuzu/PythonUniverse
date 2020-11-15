# Lambda Functions

## Table of Contents
* [Lambda Functions](#lambda-functions)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
    * [General Case](#general-case)
    * [Lambda Case](#lambda-case)
  * [Usage](#usage)
    * [General Case](#general-case-1)
    * [Lambda Case](#lambda-case-1)
* [Related Articles](#related-articles)

## Basic

### General Case

``` py
def hello():
    print("Ahoy")

def sum(x, y):
    return x + y

type(hello)  # <class 'function'>
type(sum)  # <class 'function'>

hello()  # Ahoy
sum(1, 1)  # 2
```

### Lambda Case

``` py
hello = lambda: print("Ahoy")
sum = lambda x, y: x + y

type(hello)  # <class 'function'>
type(sum)  # <class 'function'>

hello()  # Ahoy
sum(1, 1)  # 2
```

## Usage

The Lambda function is ideal for map, reduce, filter, and other built-in functions as a conditional function. In the following example, let's take the [map function](map.md) as an example and make all the values in the list 10 times.

### General Case

``` py
def mul_10(x):
    return x * 10

li = [1, 2, 3]
li = [*map(mul_10, li)]

# li = [10, 20, 30]
```

### Lambda Case

``` py
li = [1, 2, 3]
li = [*map(lambda x: x * 10, li)]

# li = [10, 20, 30]
```

# Related Articles

| Article                                                | Link                                                                                        |
| ------------------------------------------------------ | ------------------------------------------------------------------------------------------- |
| Python進階技巧 (4) — Lambda Function 與 Closure 之謎！ | https://medium.com/citycoddee/python進階技巧-4-lambda-function-與-closure-之謎-7a385a35e1d8 |
| 5 Python tricks that will improve your life [6:34]     | https://youtu.be/5tcs2qXP3Pg?t=394                                                          |
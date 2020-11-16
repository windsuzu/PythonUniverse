# Generator

Lists need to read all the elements at once, which is memory intensive when the list is too large, and generator solves this problem. Generator is an implementation of iterator with **lazy evaluation features**, which can reduce memory usage very effectively. 

## Table of Contents

* [Generator](#generator)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
    * [Old](#old)
    * [Create a generator object](#create-a-generator-object)
    * [Iterate the generator](#iterate-the-generator)
      * [next()](#next)
      * [for-each](#for-each)
  * [send()](#send)
  * [Advantages](#advantages)
    * [Access with List](#access-with-list)
    * [Access with Generator](#access-with-generator)

## Basic

We hope that when we collect data in the for-loop, we don't want to wait until all the data is collected and then return it to the client, but give it to the client every time we collect it.

### Old

``` py
def give_client_an_updated_list(nums):
    result = []
    for i in nums:
        result.append(i**2)
    return result

give_client_an_updated_list([1, 2, 3, 4, 5])
# [1, 4, 9, 16, 25]
```

### Create a generator object

We can use a generator to do this.

``` py
def give_client_an_updated_list(nums):
    for i in nums:
        yield i**2
```

### Iterate the generator

There are two ways to retrieve the data from the generator, either by `next()` or by using a for-each syntax.

#### next()

``` py
gen = give_client_an_updated_list([1, 2, 3, 4, 5])

type(gen)  # generator
next(gen)  # 1
next(gen)  # 4
next(gen)  # 9
next(gen)  # 16
next(gen)  # 25
next(gen)  # Error: StopIteration
```

#### for-each

``` py
for num in gen:
    print(num)

# 1
# 4
# 9
# 16
# 25
```

## send()

I don't know much about the usage of `generator.send()`, but here is a detailed explanation of its usage and why it is used.

> [python generator “send” function purpose?](https://stackoverflow.com/questions/19302530/python-generator-send-function-purpose)

## Advantages

Next, we will show the advantages of generator and why it is used instead of reading the list.

### Access with List 

``` py
%load_ext memory_profiler
def give_client_an_updated_list(value):
    res = []
    for i in range(value):
        res.append(i**2)
    return res
```

``` py
%%time
%%memit
li = give_client_an_updated_list(10_000_000)

# will pause for 3 seconds before proceeding to the following task.

...
...
```

Not only does it take a lot of time to load all the data before it can continue to run, it also uses a lot of memory to access it.

```
peak memory: 440.75 MiB, increment: 385.73 MiB
Wall time: 3.84 s
```

### Access with Generator 

``` py
%load_ext memory_profiler
def give_client_an_updated_list(value):
    for i in range(value):
        yield i**2
```

``` py
%%time
%%memit
li = give_client_an_updated_list(10_000_000)

# almost no waiting.

...
...
```

```
peak memory: 53.36 MiB, increment: 0.00 MiB
Wall time: 0 ns
```

Because the generator doesn't read everything down, it reads it when you need it. So he barely uses any memory space or spends any time on it.
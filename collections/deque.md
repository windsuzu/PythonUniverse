# Deque

You can think of a `deque` as a list with the functionality of insert and pop items from both front and back, and it can also do the rotation.

## Table of Contents

* [Deque](#deque)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
  * [Usage](#usage)
* [Related Articles](#related-articles)

## Basic

First, the `deque` can be treated as a `list`, the methods `append()`, `extend()`, and `pop()` work as usual.

``` py
d = deque()
d.append(1)
# deque([1])

d.extend([2, 3])
# deque([1, 2, 3])

d.pop()  # 3
# deque([1, 2])
```

But, here comes the skills that only `deque` has, the methods `appendleft()`, `extendleft()`, and `popleft()` can insert and pop the elements from the beginning of the `deque`.

> Be careful that the method `extendleft()` will reverse the order of input

``` py
d = deque()
d.extendleft([1, 2])
# deque([2, 1])

d.appendleft(3)
# deque([3, 2, 1])

d.popleft()  # 3
# deque([2, 1])
```

`deque` also has a method `rotate()` to rotate itself. If you call it with a positive integer, it will perform a **right rotation**; if you call it with a negative integer, it will perform a **left rotation**. 

``` py
d = deque([1, 2, 3, 4])
d.rotate(1)
# deque([4, 1, 2, 3])

d.rotate(-2)
# deque([2, 3, 4, 1])
```

## Usage

This is a `deque` example from Python documentation, it uses the `deque` to maintain a list of elements by `appending to the right` and `popping to the left`.

``` py
def moving_average(iterable, n=3):
    # moving_average([40, 30, 50, 46, 39, 44]) --> 40.0 42.0 45.0 43.0
    # http://en.wikipedia.org/wiki/Moving_average
    it = iter(iterable)
    d = deque(itertools.islice(it, n-1))
    d.appendleft(0)
    s = sum(d)
    for elem in it:
        s += elem - d.popleft()
        d.append(elem)
        yield s / n
```

# Related Articles

| Article                                  | Link                                                                 |
| ---------------------------------------- | -------------------------------------------------------------------- |
| collections - deque                      | https://docs.python.org/3/library/collections.html#collections.deque |
| Python deque用法介绍                     | https://blog.csdn.net/liangguohuan/article/details/7088265           |
| The Complete Python Course For Beginners | https://youtu.be/sxTmJE4k0ho?list=LL&t=16357                         |
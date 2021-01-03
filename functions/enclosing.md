# Enclosing Functions

Enclosing function simply means that the function returns a function. It can be extended to the use of [decorator](../assets/must_know/closure_decorator.png), but this is a brief introduction to the enclosing function.

## Table of Contents

* [Enclosing Functions](#enclosing-functions)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
  * [Enclosing Function](#enclosing-function)
* [Related Articles](#related-articles)

## Basic

When you have an addition function, fill in `a`, `b` and get `c`, but for the time being you only need to change `a`, and `b` are 5, so you might use the default parameter `b=5`

``` py
def add(a, b=5):
    return a + b

add(3)  # 8
add(4)  # 9
add(5)  # 10
```

This method has to be rewritten once when `b` needs to be changed, which is obviously not very good.

## Enclosing Function

This is when the enclosing function comes into play.

``` py
def add_withb(b):
    def add(a):
        return a + b
    return add


add4 = add_withb(4)
add4(3)  # 7
add4(7)  # 11


add5 = add_withb(5)
add5(4)  # 9
add5(5)  # 10
```


# Related Articles

| Article                          | Link                                                                     |
| -------------------------------- | ------------------------------------------------------------------------ |
| [python] Why Enclosing Function? | http://blog.ittraining.com.tw/2019/12/python-why-enclosing-function.html |

# Dynamic Language

Thanks to the dynamic nature of python, we can define functions in loops or conditions.

But this feature is usually useless. ಠ_ಠ

## Table of Contents

* [Dynamic Language](#dynamic-language)
  * [Table of Contents](#table-of-contents)
  * [For-loop def](#for-loop-def)
  * [Conditional def](#conditional-def)


## For-loop def

Only last function will be left.

``` py
for i in range(10):
    def say():
        print(i)
    say()  # 0, 1, 2, 3, 4, 5, 6, 7, 8, 9

say()  # 9
```

## Conditional def

This is a little more practical than for-loop. 

``` py
def returnFunc(a):
    if a < 100:
        def mul(b):
            print(a * b)
        return mul
    else:
        def add(b):
            print(a + b)
        return add

mul = returnFunc(10)
mul(10)  # 100

add = returnFunc(100)
add(10)  # 110
```
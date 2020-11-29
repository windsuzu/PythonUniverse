# Dynamic Language

Because python is a dynamic language, there are many things that other languages can't do, and this is also mentioned in the documentation: [9.7. Odds and Ends](https://docs.python.org/3/tutorial/classes.html#odds-and-ends).

## Table of Contents

* [Dynamic Language](#dynamic-language)
  * [Table of Contents](#table-of-contents)
  * [Define class in condition](#define-class-in-condition)
  * [Define class in For-loop](#define-class-in-for-loop)
  * [Pre-defined in class](#pre-defined-in-class)
  * [Post-defined Class variables](#post-defined-class-variables)
  * [Post-defined Instance variables](#post-defined-instance-variables)

## Define class in condition

<!-- TODO: link to function in condition -->

We can define a class inside a function, and even create a class by using condition (if-else). Of course, you can also [create functions by condition]().

``` py
def getClass(x):
    if x == 1:
        class ClassA:
            x = 1
        return ClassA
    else:
        class ClassB:
            x = 0
        return ClassB
    
cls = getClass(1)
print(cls)    # <class '__main__.getClass.<locals>.ClassA'>
print(cls.x)  # 1
```

## Define class in For-loop

We can also create classes in a loop and keep the last class created when we leave.

``` py
for i in range(10):
    class ClassA:
        x = i
        
    cls = ClassA()
    print(cls.x)  # 0, 1, 2, 3, 4, 5, 6, 7, 8, 9

print(cls.x)  # 9
```

## Pre-defined in class

We can define [class variables and instance variables](variables_class_instance.md) in class early, and then use them outside when they are ready.

``` py
class Example:
    def hi(self):
        print(Example.cls_var)
        print(self.inst_var)


e = Example()
Example.cls_var = "ya"
e.inst_var = "wow"

e.hi()  # ya, wow
```

## Post-defined Class variables

We can implement `class variables` after defining class.

``` py
class Example:
    pass

Example.cls_a = 1

e = Example()
print(e.cls_a)  # 1
```


## Post-defined Instance variables

We can implement `instance variables` after defining class.

``` py
class Example:
    pass

e = Example()
e.msg = "wow"
e.hi = lambda self: print(self.msg)

e.hi(e)  # wow
```
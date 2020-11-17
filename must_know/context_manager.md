# Context Manager

Have you ever seen the following code for accessing data?

``` py
with open('sample.txt', 'w') as f:
    f.write('test')
```

This is actually a usage of context manager.

## Table of Contents

* [Context Manager](#context-manager)
  * [Table of Contents](#table-of-contents)
  * [Basic](#basic)
    * [Class Context Manager](#class-context-manager)
    * [Function Context Manager](#function-context-manager)
    * [Practice](#practice)


## Basic

The Context Manager helps us **initialize** and automate the required actions at the **end** of the process.

For example, the common use of `file()` is to open a file, read the file and finally close the file variable.

``` py
f = open('sample.txt', 'w')
f.write('test')
f.close()
```

### Class Context Manager

So to design a context manager, we have to handle the **initialization of the object**, then **return the object** to the user for a period of time, and finally handle the **termination of the object** for the user.

Let's simulate the `open()` context manager. To create a context manager using class, you need to give it two methods:

1. `__enter__`: initialize and return the file object
2. `__exit__`: handle the termination of the file object

``` py
class OpenFile():
    def __init__(self, filename: str, mode: str) -> object:
        self.filename = filename
        self.mode = mode

    def __enter__(self):
        self.file_obj = open(self.filename, self.mode)
        return self.file_obj

    def __exit__(self, except_type, except_val, except_traceback):
        self.file_obj.close()
```

Then you can use `OpenFile` as an object that can be manipulated by the context manager, just like `open()`.

``` py
with OpenFile('sample.txt', 'r') as f:
    print(f.read())
```

### Function Context Manager

Another way to create a context manager is to use the function, which combines the [generator](generator.md) and [decorator](closure_decorator.md) interactions! If you don't know generator or decorator yet, click on them to see the tricks.

First, import `contextlib.contextmanager` and add it as a decorator on the head of the function that needs to be managed by `contextmanager`. Then, use the generator's `yield` to return the desired object to the user, similar to `__enter__`. Finally, all operations after `yield` are treated as operations in `__exit__`.

``` py
from contextlib import contextmanager

@contextmanager  # <---------------- decorator
def openfile(filename, mode):
    f = open(filename, mode)
    yield f  # <-------------------- generator
    f.close()


with openfile('sample.txt', 'r') as f:
    print(f.read())
```

We can add `try-except-else-finally` to the function to prevent I/O errors.

``` py
from contextlib import contextmanager

@contextmanager
def openfile(filename, mode):
    try:
        f = open(filename, mode)
        yield f
    
    finally:
        f.close()
```

### Practice

Let's demonstrate the benefits of `contextmanager` with a real case study. 

For example, we want to use `os` to move to the desired path, write some files and store them there, and then use `os` again to go back to the original path.

Then do it again, this time to a different folder. and again, and again...

``` py
import os

home = os.getcwd()
os.chdir('folder1')
with open('example1.txt', 'w') as f:
    f.write('file1')
os.chdir(home)

home = os.getcwd()
os.chdir('folder2')
with open('example2.txt', 'w') as f:
    f.write('file2')
os.chdir(home)
```

In the above example, the user only knows that the syntax `with open` can be used, but has no idea about the concept of context manager. So let's help him to create a function `enterFolder` that can be managed by context manager!

``` py
@contextmanager
def enterFolder(folderName):
    home = os.getcwd()
    os.chdir(folderName)
    yield
    os.chdir(home)
```

Now, we can simplify the original code to the following expression.

``` py
with enterFolder('folder1'):
    with open('example1.txt', 'w') as f:
        f.write('file1')

with enterFolder('folder2'):
    with open('example2.txt', 'w') as f:
        f.write('file2')
```

After **Python 3.1**, you can also put more than one action inside the `with` syntax.

``` py
with enterFolder('folder1'), open('example1.txt', 'w') as f:
    f.write('file1')

with enterFolder('folder2'), open('example2.txt', 'w') as f:
    f.write('file2')
```
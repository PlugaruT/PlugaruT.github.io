---
title: Abstract methods in Python
layout: post
projects: false
category: blog
author: tudor
externalLink: false
---

An abstract method is a method defined inside a base class but without an implementation.
The popular way to declare an abstract method in Python is to use `NotImplementedError` exception:
```python
class Foo:
    def my_abstract_method(self):
        raise NotImplementedError
```

We declare another class `Bar` that inherits from `Foo` and we don't override the abstract method.

```python
>>> Bar()
<__main__.Bar at 0x7f7c94380828>

>>> Bar().my_abstract_method()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 3, in my_abstract_method
NotImplementedError
```

A better way of doing this is raising the error when the object is being instantiated using the built-in module `abc`.

```python
from abc import ABCMeta, abstractmethod

class AFoo(metaclass=ABCMeta):
    @abstractmethod
    def my_abstract_method(self):
        pass
```

And when we will try to instantiate a class that inherits from `AFoo` without implementing the abstract method, the error will be raised when we try to instantiate an object.

```python
# Assume that class Bar inherits from AFoo
>>> Bar()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't instantiate abstract class Bar with abstract methods my_abstract_method
```
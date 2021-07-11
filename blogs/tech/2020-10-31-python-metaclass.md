---
title:  "python metaclass"
description: "python metaclass"
date: 2020-10-07 15:04:23
hidden: false
categories: [Tech]
tags: [python, ruby]
---

# Python Metaclass

huh... metaclass, isn't it the **singleton class** in ruby?

Just feel more and more the same for Ruby and Python in the class of class, everything is an object, etc.

[WOW](https://stackoverflow.com/questions/100003/what-are-metaclasses-in-python?answertab=votes#tab-top)...

## In python 2 

```
class Foo(Bar):
    pass
```

Python will look for __metaclass__ in the class definition. If it finds it, it will use it to create the object class Foo. If it doesn't, it will use type to create the class.

1. Is there a __metaclass__ attribute in Foo?
2. If yes, create in-memory a class object (I said a class object, stay with me here), with the name Foo by using what is in __metaclass__.
3. If Python can't find __metaclass__, it will look for a __metaclass__ at the MODULE level, and try to do the same (but only for classes that don't inherit anything, basically old-style classes).
4. Then if it can't find any __metaclass__ at all, it will use the Bar's (the first parent) own metaclass (which might be the default type) to create the class object.

Be careful here that the __metaclass__ attribute will not be inherited, the metaclass of the parent (Bar.__class__) will be. If Bar used a __metaclass__ attribute that created Bar with type() (and not type.__new__()), the subclasses will not inherit that behavior.


## Metaclasses in Python 3

The syntax to set the metaclass has been changed in Python 3:

```
class Foo(object, metaclass=something, kwarg1=value1, kwarg2=value2):
    ...
```

## Others 

https://cloud.tencent.com/developer/article/1546310
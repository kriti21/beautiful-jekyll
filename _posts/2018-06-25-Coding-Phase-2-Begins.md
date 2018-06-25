---
layout: post
title: GSoC Coding Phase 2 Begins 
tags: [Google Summer of Code, open-source, coala]
---

This is probably too late to write this but I have passed Coding phase 1. Yay!! But honestly I must say the credit goes to my mentors for being so understanding with me. Even though my tasks for coding phase 1 are yet to be completed, they considered the fact that I had exams during coding phase 1. And this very well points out the fact that, this time no delay would be acceptable. So I am all pumped up for this phase. :P

Before we start with my tasks for coding phase 2, let's do quick check on what I have done so far and readers might find something to learn as well. :)

- Implemented code to enable `GitCommitBear` to detect GitHub PR merge commits and ignore them. It runs on the unmerged parent of these commits instead. The main challenge in this task was not implementing the required changes but rather writing tests for those changes. Testing is one crucial skill that I am learing for the very first time in my life and damn, it's quite a tough challenge.

- Implemented code for meta bear `VCSCommitBear` that does analysis on git commits such as determining if the commit tries to escape CI build, the type of special commit it is viz. `git merge` or `git revert` commit, and also the files added, modified or deleted by the commit. This meta bear returns a HiddenResult that would not be seen by the users. Instead this meta bear would be used by other bears for further inspection of each type of special commit. Details about these commits will be given in future posts :P

Main challenge in this task is again testing. Well this is a new experience for me, may be that's why. But I am learning a lot, that's a sure thing. 

So while I have been working on `VCSCommitBear`, (the code for which by the way is available [here](https://github.com/coala/coala-bears/pull/2543) You can probably see how many comments there are just to get the tests right) I have learnt about some new things that I didn't know before. One of them is MRO and this is what I shall discuss here.

## Method Resolution Order or MRO

Before we dive into what MRO is, let's first do a quick check on different type of inheritance in Python. When a class is derived from more than one base classes, it is called **multiple** inheritance.
Example:
```python
   class Base1:
       pass

   class Base2:
       pass

   class MultiDerived(Base1, Base2):
       pass
```

Here, `MultiDerived` is derived from classes `Base1` and `Base2`.

A class can also be inherited form a derived class. This is called **multilevel** inheritance. It can be of any depth in Python. In multilevel inheritance, features of the base class and the derived class is inherited into the new derived class.
Example:
```python
   class Base:
       pass
   
   class Derived1(Base):
       pass
   
   class Derived2(Derived1):
       pass
```

Here, `Derived1` is derived from `Base`, and `Derived2` is derived from `Derived1`.

Now consider the following inheritance scenario:

```python
   class Base1:
       pass

   class Base2:

       def foo(self):
           print 'B2-foo'

       def bar(self):
           print 'B2-bar'
```

```python
   class MultiDerived1(Base1, Base2):
       pass

   class MultiDerived2(Base1, Base2):

       def bar(self):
           print 'MD2-bar'
```

```python
   class MultiDerived3(MultiDerived1, MultiDerived2:
       pass
```

*Old Style Class vs New Style Class*

In old style class, if we create an object of class `MultiDerived3` and call functions, following output is obtained:
```
>>>obj = MultiDerived3()
>>>obj.foo()
B2-foo
>>>obj.bar()
B2-bar
```

However, in new style class the output is quite different as:
```
>>>obj = MultiDerived3()
>>>obj.foo()
B2-foo
>>>obj.bar()
MD2-bar
```

As you can see, the output for `obj.bar()` differs. So what happened here? In the multiple inheritance scenario, any specified attribute is searched first in the current class. If not found, the search continues into parent classes in depth-first, left-right fashion without searching same class twice. So, in the above example of `MultiDerived3` class the search order is [`MultiDerived3`, `MultiDerived1`, `Base1`, `Base2`, `MultiDerived2`, `object`]. That is why the output of `obj.bar()` is `B2-bar`. 

However, if you see carefully, the precedance should be more for `MultiDerived2` than `Base1` and `Base2`.
By drawing a hierarchy tree, one can easily observe that `MultiDerived2` is more closely related to `MultiDerived3` and hence it should be searched first. So the search order should be [`MultiDerived3`, `MultiDerived1`, `MultiDerived2`, `Base1`, `Base2`, `object`] which is implemented in new style classes in Python. That is why the output of `obj.bar()` in new style class is `MD2-bar`. This order is also called linearization of MultiDerived class and the set of rules used to find this order is called **Method Resolution Order (MRO)**.

This is just an overview of what MRO is. For more detail, [this](https://medium.com/technology-nineleaps/python-method-resolution-order-4fd41d2fcc) is great blog post you can read.

That's all for this post. Thanks for stopping by. Happy Coding :) 
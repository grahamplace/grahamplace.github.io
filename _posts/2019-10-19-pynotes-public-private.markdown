---
title: "🐍Pynotes - Public and Private and Protected, Oh My!"
layout: post
date: 2019-10-19 23:04
tag: [python]
headerImage: false
description: ""
category: blog
author: grahamplace
externalLink: false
---
_Based on Effective Python (Brett Slatkin), Chapter 3, Item 27: Prefer Public Attributes Over Private Ones_

Python supports two types of visibility for a class's attributes: **public** and **private**.

#### Public
Public attributes of an object can be accessed directly using the dot operator, e.g. `my_obj.value`.


#### Private
Private attributes are prefixed with a dunder, e.g. `__value`. Such attributes _cannot_ be accessed using the dot operator on an object. `MyClass.__value` raises an `AttributeError`.

Methods of the containing class _can_ access private attributes, e.g.

Note that the implementation of private attributes in Python does technically allow dot operator access like so: `my_obj._MyClass__value`.


#### Protected
So-called "protected" attributes in Python are public attributes prefixed with a _single_ underscore. Because they are public, they can be accessed directly with the dot operator, but per the Pep 8 style guide, the single underscore indicates callers to "proceed with caution!"


#### Example Code

```python
class Employee:
	def __init__(self):
		self.name = 'Graham'
		self._email = 'graham@email.com'
		self.__ssn = '123-12-1234'


employee = Employee()
print(f'Public value (name): {employee.name}')
print(f'Protected value (email): {employee._email}')
print(f'Private value (ssn): {employee._Employee__ssn}')
try:
	print(f'Private value (ssn): {employee.__ssn}')
except AttributeError as e:
	print(f'When trying to reference private attribute directly:\n{e}')
```

Shell script first line
-----------------------
```python
 #!/usr/bin/env python
```


Set source code encoding
------------------------
```python
# -*- coding: iso-8859-15 -*-
currency = u"€"
```


Strings
-------
```python
"multiline\nstring"
'not multiline\nstring'
'abc' * 3
'ab' + 'c' == 'a' + 'bc'
' ab '.strip() == 'ab'
word[4]
word[2:]
word[:-2]
len(word)
u'this is a unicode string'
```


lists
-----
```python
# replace some items
a[0:2] = [1, 12]
# remove some
a[0:2] = []
# insert some
a[1:1] = [1, 12]
# clear
a[:] = []
# insert a copy of itself at the beginning
a[:0] = a
# length 
len(a)
```


list and dictionary iteration
-----------------------------
```python
for x in ['cat', 'dog']:
    print x, len(x)

for i in range(a):
    print i, a[i]
    #pass
    #continue
    #break

for k, v in d.items():
    print k, v
```


formal, positional, and keyword arguments
-----------------------------------------
```python
def mymethod(arg1, arg2, *args, **kwargs):
    pass
```

* `arg1`, `arg2` : "formal" arguments
* `*args` : a ''tuple'' containing the positional arguments beyond the formal parameter list
* `**kwargs` : a ''dictionary'' of all keywords except for those corresponding to a formal parameter

* More examples:
```python
# arbitrary argument lists
def fprintf(file, format, *args):
    file.write(format % args)

# unpacking argument lists
range(3, 6)
args = [3, 6]
range(*args)

def parrot(voltage, state='a stiff'):
    pass

d = { 'voltage': 'four million', 'state': "bleedin' demised" }
parrot(**d)
```


lambda forms
------------
```python
>>> def make_incrementor(n):
...     return lambda x: x + n
...
>>> f = make_incrementor(42)
>>> f(0)
42
>>> f(1)
43
```


documentation strings (doc strings)
-----------------------------------
```python
def parrot():
    """Summary starts with capital letter and ends with period.

    Detailed text.
    """
```


built-in functions for list operations
--------------------------------------
* `filter(function, sequence)`
* `map(function, sequence)`
* `reduce(function, sequence)`


list comprehensions
-------------------
```python
>>> freshfruit = ['  banana', '  loganberry ', 'passion fruit  ']
>>> [weapon.strip() for weapon in freshfruit]
['banana', 'loganberry', 'passion fruit']

>>> vec = [2, 4, 6]
>>> [3*x for x in vec]
[6, 12, 18]

>>> [(x, x**2) for x in vec]
[(2, 4), (4, 16), (6, 36)]

>>> vec1 = [2, 4, 6]
>>> vec2 = [4, 3, -9]
>>> [x*y for x in vec1 for y in vec2]
[8, 6, -18, 16, 12, -36, 24, 18, -54]
>>> [x+y for x in vec1 for y in vec2]
[6, 5, -7, 8, 7, -5, 10, 9, -3]
>>> [vec1[i]*vec2[i] for i in range(len(vec1))]
[8, 12, -54]

# create new dict from otherdict but only with keys that have non-null value
dd = dict([(k, v) for k, v in otherdict.items() if v is not None])
```


deleting elements from lists by index
-------------------------------------
```python
del a[0]
del a[2:4]
del a[:]
```


tuples
------
```python
t = 1, 2, 3
t = t, (1, 2)
empty = ()
singleton = 'hello',    # <-- note trailing comma
```


sets
----
```python
>>> basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
>>> fruit = set(basket)               # create a set without duplicates
>>> fruit
set(['orange', 'pear', 'apple', 'banana'])
>>> 'orange' in fruit                 # fast membership testing
True
>>> 'crabgrass' in fruit
False

>>> a = set('abracadabra')
>>> b = set('alacazam')
>>> a                                  # unique letters in a
set(['a', 'r', 'b', 'c', 'd'])
>>> a - b                              # letters in a but not in b
set(['r', 'd', 'b'])
>>> a | b                              # letters in either a or b
set(['a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'])
>>> a & b                              # letters in both a and b
set(['a', 'c'])
>>> a ^ b                              # letters in a or b but not both
set(['r', 'd', 'b', 'm', 'z', 'l'])
```


dictionaries
------------
```python
tel = {}
tel = {'jack': 4098, 'sape': 4139}
tel['guido'] = 4127
tel.keys()
tel.has_key('guido')
tel = dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
```


looping over dictionaries and lists
-----------------------------------
```python
knights = {'gallahad': 'the pure', 'robin': 'the brave'}
for k, v in knights.items():
    print k, v

for i, v in enumerate(['tic', 'tac', 'toe']):
    print i, v

questions = ['name', 'quest', 'favorite color']
answers = ['lancelot', 'the holy grail', 'blue']
for q, a in zip(questions, answers):
    print 'What is your %s?  It is %s.' % (q, a)

# loop over in reverse, without changing the source
for i in reversed(xrange(1,10,2)):
    print i

# loop over in sorted order, without changing the source
basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
for f in sorted(set(basket)):
    print f
```


some interesting comparisons
----------------------------
```python
>>> string1, string2, string3 = '', 'Trondheim', 'Hammer Dance'
>>> non_null = string1 or string2 or string3
>>> non_null
'Trondheim'

(1, 2, 3)              < (1, 2, 4)
[1, 2, 3]              < [1, 2, 4]
'ABC' < 'C' < 'Pascal' < 'Python'
(1, 2, 3, 4)           < (1, 2, 4)
(1, 2)                 < (1, 2, -1)
(1, 2, 3)             == (1.0, 2.0, 3.0)
(1, 2, ('aa', 'ab'))   < (1, 2, ('abc', 'a'), 4)
```

To be continued from Section 6: Modules:
http://www.python.org/doc/current/tut/node8.html


How to force specific version with easy_install or pip
------------------------------------------------------
```
easy_install lxml==2.2.8
pip install lxml==2.2.8
```

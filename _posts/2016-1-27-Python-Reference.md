---
layout: post
title: Python Reference
update: 2016-2-15

---

Python 3.x, 2.x reference.

# Python 3.x

```
#!/usr/bin/env python3
# tell the system this is an python executable
#-*- coding: utf-8 -*-
# tell python interpreter to read the file in UTF-8
```

```
python3 -m pdb err.py
> /some/path/err.py<module>()
-> some line
(Pdb) l
# show current line
(Pdb) n
# execute single line
(Pdb) p variable
# show variable
(Pdb) q
# exit pdb

# in err.py
import pdb
pdb.set_trace()
# set break point

```

### type

**built-in types:**
numerics, sequences, mappings, files, classes, instances and exceptions.

```
>>> x = 'abc'
>>> y = 123
>>> isinstance(x, str)
True
>>> isinstance(y, str)
False

test = float("inf") # infinite number
```
凡是可作用于`for`循环的对象都是`Iterable`类型；

凡是可作用于`next()`函数的对象都是`Iterator`类型，它们表示一个惰性计算的序列；

集合数据类型如`list`、`dict`、`str`等是`Iterable`但不是`Iterator`，不过可以通过`iter()`函数获得一个`Iterator`对象。

```
>>> from collections import Iterable
>>> isinstance([], Iterable)
True
>>> isinstance({}, Iterable)
True
>>> isinstance('abc', Iterable)
True
>>> isinstance((x for x in range(10)), Iterable)
True
>>> isinstance(100, Iterable)
False

>>> from collections import Iterator
>>> isinstance((x for x in range(10)), Iterator)
True
>>> isinstance([], Iterator)
False
>>> isinstance({}, Iterator)
False
>>> isinstance('abc', Iterator)
False

>>> isinstance(iter('abc'), Iterator)
True
```

type() function

```
>>> import types
>>> def fn():
...     pass
...
>>> type(fn)==types.FunctionType
True
>>> type(abs)==types.BuiltinFunctionType
True
>>> type(lambda x: x)==types.LambdaType
True
>>> type((x for x in range(10)))==types.GeneratorType
True
```

### IO
```
>>> 'Hi, %s, you have $%d.' %('Michael', 1000000)
'Hi, Michael, you have $1000000.'

>>> '%2-%02' % (3, 1)
' 3-01'

>>> 'growth rate: %d %%' % 7
'growth rate: 7 %'
```

### File IO
```
# read from file
try:
    f = open('/path/to/file', 'r')
    print(f.read())
finally:
    if f:
        f.close()

with open('/path/to/file', 'r') as f:
    print(f.read())
# no need for f.close

for line in f.readlines():
    print(line.strip())
   
# binary file 
f = open('/Users/micheal/test.jpg', 'rb')
f.read()
b'\xff\xd8\...'

# encoding
f = open('/User/michael/gbk.txt', 'r', encoding='gbk', errors='ignore')
f.read()

# write to file
f.open('/Users/michael/test.txt', 'w')
f.write('Hello, world!')
f.close()
# write no guaranteed to finish until f.close()

with open('/Users/michael/test.txt', 'w') as f:
f.write('Hello, workd!')
```

### list

```
>>> classmates = ['A', 'B', 'C']
>>> classmates[-1]
'C'
>>> classmates[-2]
'B'

>>> classmates.append('D)
>>> classmates.insert(1, '1')
>>> classmates
['A', '1', 'B', 'C', 'D']

>>> classmates.pop()
'D' # delete last element
# remove ith item from list and return it. remove last one if index not provided
>>> classmates.pop(1)
'1'
>>> classmates
['A', 'B', 'C']

>>> list.remove(x)
# remove the first item from the list whose value is x

list.sort()
# returns nothing, sort the list in place
sorted(li)
# return a copy of sorted li

#slice
>>> L = list(range(100)) # 0 ~ 99
>>> L[:10]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> L[-10:]
[90, 91, 92, 93, 94, 95, 96, 97, 98, 99]
>>> L[:10:2]
[0, 2, 4, 6, 8]

#loop
>>> for i, value in enumerate(list):
...     do sth

#list comprehension
>>> [x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]

>>> [m + n for m in 'ABC' for n in 'XYZ']
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']

```

### tuple  
tuple can't be modified after initialization

```
>>> classmates = ['A', 'B', 'C']

>>> t = () # empty tuple
>>> t
()

>>> t = (1,) # tuple with 1 element
>>> t
(1,)

>>> t = ('a', 'b', ['A', 'B'])
>>> t[2][0] = 'X'
>>> t[2][1] = 'Y'
>>> t
('a', 'b', ['X', 'Y'])

>>> for x, y in [(1, 1), (2, 4), (3, 9)]:
...     print(x, y)
...
1 1
2 4
3 9
```

### dict
key is immutable 

```
>>> d.get(key)
>>> d.get(key, -1)
-1
# if key doesn't exist, return None or specified value

#delete key
d.pop(key)

#loop
>>> for value in d.values():
>>> for k, v in d.items():
```

### set
unique and unordered collection of keys

```
>>> s = set([1, 2, 3])
>>> s
{1, 2, 3}
>>> s.add(4)
>>> s.remove(4)
```

### string
`\` (back slash) is used to escape characters.


```
>>> 'AAA'.title()
'Aaa'


```

### sort

```
>>> sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower, reverse=True)
['Zoo', 'Credit', 'bob', 'about']

>>> sorted(['a', 'aa', 'aaa'], key=len, reverse=True)
['aaa', 'aa', 'a']
```

### rand

```
import random
random.seed()
random.randint(start, end) # [start, end] inclusive
```

### map,reduce

```
>>> list(map(str, [1,2,3]))
['1', '2', '3']

>>> from functools import reduce

>>> reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)
```


### function

\# function returns a tuple

```
import math

def move(x, y, step, angle=0):
    nx = n + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny

>>> x, y = move(100, 100, 60, math.pi/6)
>>> print(x, y)
151.96152422706632 70.0
>>> r = move(100, 100, 60, math.pi/6)
print(r)
(151.96152422706632 70.0)
```

\# default arguments must follow other variables

```
def power(x, n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
    
>>> power(5)
25
>>> power(5, 2)
25

def enroll(name, gender, age=6, city='Beijing');
    ...

>>> enroll('Bob', 'M', 7)
>>> enroll('A', 'M', city='Tianjin')
```

\# default arguments must be immutable

```
# bad example
def add_end(L=[]):
    L.append('END')
    return L

>>> add_end()
['END']
>>> add_end()
['END', 'END']
...

# fix bad example
def add_end(L=None):
    if L is None:
        L = []
    L.append('END')
    return L

```

\# mutable arguments

```
# a^2 + b^2 + c^2 + ...
def calc(numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
    
>>> calc([1,2,3])
14

def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
    
>>> calc(1,2)
5
>>> calc()
0
>>> nums = [1,2,3]
>>> calc(*nums)
14

```

\#keyword argument

```
def person(name, age, *, city, job):
    ...
    
>>> person('Jack', 24, city='Beijing', job='Engineer')

def person(name, age, *, city='Beijing', job):
    ...
    
>>> person('Jack', 24, job='Engineer')
```

### scope
* public: `abc`, `x123`, `PI`...
* special variable: `__xxx__`, `__name__`, `__author__`...
* private: `_xxx`(can be accessed from outside, but by convention seen as private), `__xxx`...


### OOP

```
super(type[, object-or-type])

Return a proxy object that delegates method calls to a parent or sibling class of type.

In a class hierarchy with single inheritance, super can be used to refer to parent classes without naming them explicitly, thus making the code more maintainable.

```

---
---
---



# Python 2.x
`sys.exit()`

`format = 'AM' if s.find('AM') else 'PM'`

### IO

```
#read in all lines as string
import sys
lines = sys.stdin.readlines()


#read line as string
>>> raw_input()

>>> array = [int(x) for x in raw_input().split()]

>>> a, b = [int(x) for x in raw_input().split()]


#use raw_input() and eval the expression, dangerous
input()

file = open('filename', 'r')
for line in file:
    do sth
    
    
#output
>>> arr = ['a', 'b', 'c']
>>> print arr
['a', 'b', 'c']
>>> print ''.join(are)
abc
```

### type

```
True
False
None
```

type | size              | in C
-----|-------------------|-----------
int  | 32 bits ( 10^9 )  | long in C
float| 10^38             | double in C
long |unlimited precision| No

`7/4 = 1`

`7/4.0 = 1.75`

### string

```
'I\'m happy' = "I'm happy"

len('12345') = 5

s.lower() 
s.isalpha()

'[1, 2, 3, 4, 5]'.strip('[]').replace(',', '') == '1 2 3 4 5'

','.join('123') = '1,2,3'

ord('A') == 65
chr(65) == 'A'

print “.” * 10 = **********

print “”"
someting
“”"
print ‘''
something
‘''
print ‘string ’ + str(1)
print ‘string’, 1
print ‘{} {}’.format(’string’, 1) // python 2.7+
print ‘{0} {1}’.format(’string’, 1) // python 2.6-
print ‘string %d’ %(1)

format(1.1, ‘.2f’) = 1.10
format(1.234, ‘.2f’) = 1.23
format(1.235, ‘.2f’) = 1.24
for c in reversed('1234'):
    print c
#1234 -> 4321
```

### loop
```
for i, x in enumerate(list):
    print i, v

for _ in xrange(int(raw_input())):
    # handle number of test case
    
range(0, 10 3) = [0, 3, 6, 9]
```

### math
```
from math import *

factorial(3) = 6
sqrt(10) = 3.16...
```

### list
```
s = []
s.append(1) = [1]
len(s) == 1

s=[1,2,3]
s.pop() = 3 # s = [1,2]
s.pop(0) = 1 # s = [2]

list comprehension:
squares = [x**2 for x in range(10)]
squares = [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

s = [4,3,2,1]
sorted(s) = [1,2,3,4]
s[::-1] = [1,2,3,4]

# swap
list[a], list[b] = list[b], list[a]

# two dimensional array
dp = [[0 for x in range(cols)] for x in range(rows)]

dp = [[0 for x in range(3)] for x in range(5)]

dp[4][2] = 1
[[0,0,0],
 [0,0,0],
 [0,0,0],
 [0,0,0],
 [0,0,1]]

```

### dictionary
```
# create dictionary
dic = dict(
    sape=4139,
    guido=3128,
    jack=3098
)

tel = {
    1:1,
    'jack':4098,
    'sape': 4139
}
'jack' in tel == True

tel.values()
# [4098, 4139] or [4139, 4098]
tel.items()
# [('sape', 4139), ('jack', 4098)]

# add new key
tel['guido'] = 4127
# remove key
del tel[1]
```

### set
```
# empty set
a = set()

#intersection between two string:
a = set(‘123') = set(['1', '3', '2'])
b = set(‘345')
c = set(‘456')
a & b == set(‘3')
a & c == set([])
```
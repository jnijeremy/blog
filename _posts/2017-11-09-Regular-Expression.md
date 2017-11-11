---
layout: post
title: Regular Expression
update: 2017-11-09

---

# Regular Expression

## syntax
- `\d` = 1 number
- `\w` = 1 alphanum
- `\s` = 1 space
- `*` = any # chars ( including 0 char )
- `+` = at least one char
- `?` = 0 or 1 char
- `{n}` = n chars
- `{n, m}` = n ~ m chars

e.g.

- `00\d` can be `007`, but not `00A`
- `\d\d\d` can be `010`
- `\w\w\w` can be `py3`	
- `py.` can be `pyc`, `pyo`, `py!`, etc
- `.` = any char

---

e.g.

`\d{3}\s+\d{3,8}` = 任意空格隔开的带区号的电话号码

1. `\d{3}` = 3 numbers
2. `\s+` = at least one space
3. `\d{3, 8}` = 3 ~ 8 numbers

--- 

`[0-9a-zA-Z\_]` = 1 number or char or underscore

`[0-9a-zA-Z\_]+` = at least one number or char or underscore

`[a-zA-Z\_][0-9a-zA-Z\_]*` = start with 1 char or underscore, follow with any # of number, char or underscore, which is python valid variable name.

`[a-zA-Z\_][0-9a-zA-Z\_]{0, 19}` = len 1 ~ 20

`A|B` = A or B

`[P|p]ython` = `Python` or `python`

`^` = beginning of line

`^\d` = must start with number

`$` = end of line

`\d$` = must end with number

## python re module
```
>>> import re
>>> re.match(r'^\d{3}\-\d{3,8}$', '010-12345')
Match object
>>> re.match(r'^\d{3}\-\d{3,8}$', '010 12345}
None
```
`match()` method return Match object if match, None if not match.

## split string
```
>>> 'a b    c'.split(' ')
['a', 'b', '', '', '', 'c']
# can't handle continues spaces

>>> re.split(r'\s+', 'a b   c')
['a', 'b', 'c']

>>> re.split(r'[\s\,\;]+', 'a,b;; c  d')
['a', 'b', 'c', 'd']
```
# Pure Python

1. [Types](#1-types)
2. [Lists](#2-lists)
3. [Dictionaries](#3-dictionaries)
4. [Sets](#4-sets)
5. [Strings](#5-strings)
6. [Operators](#6-operators)
7. [Control Flow](#7-control-flow)
8. [Functions, Classes, Generators, Decorators](#8-functions-classes-generators-decorators)
9. [IPython](#9-ipython)
    - [magic commands](#magic-commands)

## 1. Types
```python
a = 2           # integer
b = 5.0         # float
c = 8.3e5       # exponential
d = 1.5 + 0.5j  # complex
e = 4 > 5       # boolean
f = 'word'      # string
```

## 2. Lists

```python
a = ['red', 'blue', 'green']       # manually initialization
b = list(range(5))                 # initialize from iteratable
c = [nu**2 for nu in b]            # list comprehension
d = [nu**2 for nu in b if nu < 3]  # conditioned list comprehension
e = c[0]                           # access element
f = c[1:2]                         # access a slice of the list
g = c[-1]                          # access last element
h = ['re', 'bl'] + ['gr']          # list concatenation
i = ['re'] * 5                     # repeat a list
['re', 'bl'].index('re')           # returns index of 're'
a.append('yellow')                 # add new element to end of list
a.extend(b)                        # add elements from list `b` to end of list `a`
a.insert(1, 'yellow')              # insert element in specified position
're' in ['re', 'bl']               # true if 're' in list
'fi' not in ['re', 'bl']           # true if 'fi' not in list
sorted([3, 2, 1])                  # returns sorted list
a.pop(2)                           # remove and return item at index (default last)
```

## 3. Dictionaries

```python
a = {'red': 'rouge', 'blue': 'bleu'}         # dictionary
b = a['red']                                 # translate item
'red' in a                                   # true if dictionary a contains key 'red'
c = [value for key, value in a.items()]      # loop through contents
d = a.get('yellow', 'no translation found')  # return default
a.setdefault('extra', []).append('cyan')     # init key with default
a.update({'green': 'vert', 'brown': 'brun'}) # update dictionary by data from another one
a.keys()                                     # get list of keys
a.values()                                   # get list of values
a.items()                                    # get list of key-value pairs
del a['red']                                 # delete key and associated with it value
a.pop('blue')                                # remove specified key and return the corresponding value
```


## 4. Sets

```python
a = {1, 2, 3}                                # initialize manually
b = set(range(5))                            # initialize from iteratable
a.add(13)                                    # add new element to set
a.discard(13)                                # discard element from set
a.update([21, 22, 23])                       # update set with elements from iterable
a.pop()                                      # remove and return an arbitrary set element
2 in {1, 2, 3}                               # true if 2 in set
5 not in {1, 2, 3}                           # true if 5 not in set
a.issubset(b)                                # test whether every element in a is in b
a <= b                                       # issubset in operator form
a.issuperset(b)                              # test whether every element in b is in a
a >= b                                       # issuperset in operator form
a.intersection(b)                            # return the intersection of two sets as a new set
a.difference(b)                              # return the difference of two or more sets as a new set
a - b                                        # difference in operator form
a.symmetric_difference(b)                    # return the symmetric difference of two sets as a new set
a.union(b)                                   # return the union of sets as a new set
c = frozenset()                              # the same as set but immutable
```

## 5. Strings

```python
a = 'red'                      # assignment
char = a[2]                    # access individual characters
'red ' + 'blue'                # string concatenation
'1, 2, three'.split(',')       # split string into list
'.'.join(['1', '2', 'three'])  # concatenate list into string
```

## 6. Operators

```python
a = 2             # assignment
a += 1 (*=, /=)   # change and assign
3 + 2             # addition
3 / 2             # integer (python2) or float (python3) division
3 // 2            # integer division
3 * 2             # multiplication
3 ** 2            # exponent
3 % 2             # remainder
abs(a)            # absolute value
1 == 1            # equal
2 > 1             # larger
2 < 1             # smaller
1 != 2            # not equal
1 != 2 and 2 < 3  # logical AND
1 != 2 or 2 < 3   # logical OR
not 1 == 2        # logical NOT
'a' in b          # test if a is in b
a is b            # test if objects point to the same memory (id)
```

## 7. Control Flow

```python
# if/elif/else
a, b = 1, 2
if a + b == 3:
    print('True')
elif a + b == 1:
    print('False')
else:
    print('?')

# for
a = ['red', 'blue', 'green']
for color in a:
    print(color)

# while
number = 1
while number < 10:
    print(number)
    number += 1

# break
number = 1
while True:
    print(number)
    number += 1
    if number > 10:
        break

# continue
for i in range(20):
    if i % 2 == 0:
        continue
    print(i)
```

## 8. Functions, Classes, Generators, Decorators

```python
# Function groups code statements and possibly
# returns a derived value
def myfunc(a1, a2):
    return a1 + a2

x = myfunc(a1, a2)

# Class groups attributes (data)
# and associated methods (functions)
class Point(object):
    def __init__(self, x):
        self.x = x
    def __call__(self):
        print(self.x)

x = Point(3)

# Generator iterates without
# creating all values at once
def firstn(n):
    num = 0
    while num < n:
        yield num
        num += 1

x = [i for i in firstn(10)]

# Decorator can be used to modify
# the behaviour of a function
class myDecorator(object):
    def __init__(self, f):
        self.f = f
    def __call__(self):
        print("call")
        self.f()

@myDecorator
def my_funct():
    print('func')

my_funct()
```

## 9. IPython

#### magic commands
```python
%quickref # Display the IPython Quick Reference Card
%magic # Display detailed documentation for all of the available magic commands
%debug # Enter the interactive debugger at the bottom of the last exception traceback
%hist # Print command input (and optionally output) history
%pdb # Automatically enter debugger after any exception
%paste # Execute preformatted Python code from clipboard
%cpaste # Open a special prompt for manually pasting Python code to be executed
%reset # Delete all variables/names defined in interactive namespace
%page OBJECT # Pretty-print the object and display it through a pager
%run script.py # Run a Python script inside IPython
%prun statement # Execute statement with cProfile and report the profiler output
%time statement # Report the execution time of a single statement
%timeit statement # Run a statement multiple times to compute an ensemble average execution time; useful for timing code with very short execution time
%who, %who_ls, %whos # Display variables defined in interactive namespace, with varying levels of information/ verbosity
%xdel variable # Delete a variable and attempt to clear any references to the object in the IPython internals
%pinfo <variable> # Get detailed info about variable
%env # Get and set env vars
%load <file_name> # Load external file
%pycat <file_name> # Display content of external file
%writefile <file_name> # Copy content to external file
```

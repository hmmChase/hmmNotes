# _Python_

- https://www.python.org/doc/
- https://docs.python.org/3/
- https://www.w3schools.com/python/python_reference.asp
- Object-oriented programming language

---

# _Install_

- https://www.python.org/downloads/

* Check installed version
  - `python -V`

- https://packaging.python.org/guides/installing-using-pip-and-virtualenv/
- Open terminal in admin mode if getting errors

* PIP
  - https://pypi.org/
  - A package manager for Python packages
  - `python -m pip install`
  - Upgrade pip
    - `python -m pip install —upgrade pip`
  - Type `pip install -h` to list help
  - Flags
    - `-U`, `--upgrade` Upgrade all packages to the newest available version

- virtualenv
  - https://pypi.org/project/virtualenv/
  - A tool to create isolated Python environments
  - Used to manage Python packages for different projects
  - Allows you to avoid installing Python packages globally which could break system tools or other projects
  - `python -m pip install virtualenv`
  - Initialize:
    - ``python `-m virtualenv venv`
    - Windows
      - `venv\Scripts\activate`
    - Other
      - `source venv/Scripts/activate`

* Update requirements
  - Make sure to be in virtual enviroment
  - `py -m pip install -r requirements.txt`

- autopep8
  - `pip install -U autopep8`
- pylint
  - `pip install -U pylint`

## Windows

- http://timmyreilly.azurewebsites.net/python-pip-virtualenv-installation-on-windows/

---

# _CLI_

- To enter the Python console (REPL)
  - `python`
  - `py`
- To exit the Python console
  - `ctrl z`
  - `exit()`
- To execute a Python file
  - `python script.py`

## _Options_

- `-d`
  - Provides debug output
- `-O`
  - Generates optimized bytecode (resulting in .pyo files)
- `-S`
  - Do not run import site to look for Python paths on startup
- `-v`
  - Verbose output (detailed trace on import statements)
- `-x`
  - Disable class-based built-in exceptions (just use strings); obsolete starting with version 1.6
- `-c cmd`
  - Run Python script sent in as cmd string

---

# _Data Types_

- Data types are strongly and dynamically typed
- Mixing incompatible types (e.g. attempting to add a string and a number) causes an exception

* String
  - `"Hello, world!"`
* Number
  - int
    - `1`
  - float
    - `2.8`
  - complex
    - `1j`
* Collections
  - List
  - Tuple
  - Set
  - Dictionary
* Boolean
  - `True`
  - `False`

---

# _Variables_

- Variables do not need to be declared
- Local-scoped by default

```
x = 5
y = "John"
```

- Scoping
  - `nonlocal` - To declare a non-local variable
  - `global` - To declare a global variable

---

# _Console logging_

- Python 2
  - ` print`` ``"Hello, world!" `
- Python 3
  - ` print``(``"Hello, World!"``) `

---

# _Concatenation_

- To combine both text and variables, Python uses the `+` character

```
x = "Python is "
y = "awesome"
z =  x + y
print(x + y)
# Python is awesome
```

- If you try to combine a string and a number, Python will give you an error

```
x = 5
y = "John"
print(x + y)
# TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

---

# _Casting_

- There may be times when you want to specify a type on to a variable
- Python is an object-orientated language, and as such it uses classes to define data types, including its primitive types
- Casting is done using constructor functions
- `int()`
  - Constructs an integer number from:
    - an integer literal
    - a float literal (by rounding down to the previous whole number)
    - a string literal (providing the string represents a whole number)
  - `x = int("3") # 3`
- `float()`
  - Constructs a float number from:
    - an integer literal
    - a float literal
    - a string literal (providing the string represents a float or an integer)
  - `y = float("3") # 3.0`
- `str()`
  - Constructs a string from a wide variety of data types
    - including strings, integer literals and float literals
  - `z = str(3.0) # “3.0”`

---

# _String Literals_

- Strings are sequences of single-character strings
- Square brackets `[]` can be used to access elements of the string

```
a = "Hello, World!"
print(a[1])
# e
```

- Substrings

```
b = "Hello, World!"
print(b[2:5])
# llo
```

- Any sequence-like object can be indexed by character
  - Negative indexes are used to denote items from the end of the sequence

```
"Hello"[-1]
# 'o'
```

- Any indexable item can generally also be sliced

```
"hello"[2:4]
# 'll'
```

- Escape a quote character inside a string with `\`

## Methods

- https://www.w3schools.com/python/python_ref_string.asp

- `strip()`
  - Removes any whitespace from the beginning or the end
- `len()`
  - Returns the length of a string
- `lower()`
  - Returns the string in lower case
- `upper()`
  - Returns the string in upper case
- `replace()`
  - Replaces a string with another string
- `split()`
  - Splits the string into substrings if it finds instances of the separator

---

# _Operators_

## Arithmetic

- `+` - Addition
- `-` - Subtraction
- `*` - Multiplication
- `/` - Division
- `%` - Modulus
- `**` - Exponentiation
- `//` - Floor division

## Comparison

- `==` - Equal
  - Compares the value of objects rather than their locations in memory
- `!=` - Not equal
- `>` - Greater than
- `<` - Less than
- `>=` - Greater than or equal to
- `<=` - Less than or equal to

## Assignment

- `=`
- `+=`
- `-=`
- `*=`
- `/=`
- `%=`
- `//=`
- `**=`
- `&=`
- `|=`
- `^=`
- `>>=`
- `<<=`

## Logical

- `and`
  - Returns `True` if both statements are true
  - Can be used to combine conditional statements
    - ` if``` `a > b and c > a:`
- `or`
  - Returns `True` if one of the statements is true
  - Can be used to combine conditional statements
    - ` if``` `a > b or a > c:`
- `not`
  - Reverse the result, returns `False` if the result is true

## Identity

- Tests if two variables are equal

- `is`
  - Compares object identity
  - Returns `True` if both variables are the same object
- `is not`
  - Returns `True` if both variables are not the same object

## Membership

- Checks if a value is present in a collection

- `in`
  - Returns `True` if a sequence with the specified value is present in the object

```
"a" in {"a" : 1, "b" : 2}
# True
```

- `not in`
  - Returns `True` if a sequence with the specified value is not present in the object

---

# _Keywords_

- https://www.w3schools.com/python/python_ref_keywords.asp

* `as` - To create an alias
* `assert` - For debugging
* `except` - Used with exceptions, what to do when an exception occurs
* `finally` - Used with exceptions, a block of code that will be executed no matter if there is an exception or not
* `for` - To create a for loop
* `from` - To import specific parts of a module
* `import` - To import a module
* `None` - Represents a null value
* `pass` - A null statement, a statement that will do nothing
* `raise` - To raise an exception
* `try` - To make a try...except statement
* `while` - To create a while loop
* `with` - Used to simplify exception handling
* `yield` - To end a function, returns a generator

---

# _Functions_

- A function is defined using the `def` keyword

```
def my_function():
  print("Hello from a function")
```

- To call a function, use the function name followed by parenthesis
  - `my_function()`

* Information can be passed to functions as parameters

```
def my_function(fname):
  print(fname + " Chase")

my_function("hmm")
```

- It's not possible to call a function with fewer or more arguments than they'd expect

- Default Parameter Value
  - If we call the function without an argument, it uses the default value

```
def my_function(country = "Norway"):
  print("I am from " + country)

my_function()
```

- To let a function return a value, use the `return` statement

```
def my_function(x):
  return 5 * x

print(my_function(3))
```

- You can write documentation for functions by providing a string immediately following the function signature
- This is called a `docstring`

```
def foo():
  "Does something useless"
  pass
```

---

# _Lambda_

- `lambda arguments : expression`
- A small anonymous function
- Can take any number of arguments
- Can only have one expression

```
x = lambda a, b : a * b
print(x(5, 6))
```

```
def myfunc(a, b):
  return lambda a, b : a * b
print(myfunc(5, 6))
```

```
def myfunc(n):
  return lambda a : a * n
mydoubler = myfunc(2)
print(mydoubler(11))
```

---

# _Classes/Objects_

- A Class is like an object constructor
- A "blueprint" for creating objects

* Create a class
  - `class`

```
class MyClass:
  x = 5
```

- Now we can use the class myClass to create objects

```
p1 = MyClass()
print(p1.x)
```

- All classes have a function called `__init__()`
  - Called automatically every time the class is being used to create a new object
  - Use to assign values to object properties, or other operations that are necessary to do when the object is being created

```
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

p1 = Person("John", 36)

print(p1.name)
print(p1.age)
```

- Methods
  - Functions that belongs to the object

```
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

  def myfunc(self):
    print("Hello my name is " + self.name)

p1 = Person("John", 36)
p1.myfunc()
```

- `self`
  - A reference to the class instance itself, and is used to access variables that belongs to the class
  - Has to be the first parameter of any method in the class
  - Can be named anything

```
class Person:
  def __init__(mysillyobject, name, age):
    mysillyobject.name = name
    mysillyobject.age = age

  def myfunc(abc):
    print("Hello my name is " + abc.name)

p1 = Person("John", 36)
p1.myfunc()
```

- Modify Object Properties
  - `p1.age =` ```40`
- Delete Object Properties
  - ` del``` `p1.age`
- Delete Objects
  - ` del``` `p1`

---

# _Collections_

## _Sequences _

- Array-like

* Can index and slice lists and tuples, just like strings

```
["hello", "there", "dude"][-1]
# 'dude'
[1, 2, 3][1:2]
# [2]
```

- If the datatype is mutable like, you can assign to slices

```
a = [1, 2, 3, 4]
a[1:3] = [5]
a
# [1, 5, 4]
```

### List

- Ordered
- Mutable
- Allows duplicate members

```
thislist = ["apple", "banana", "cherry"]
```

- Constructor
  - Can use the `list()` constructor to make a list

```
thislist = list(("apple", "banana", "cherry"))
print(thislist)
```

- Methods:
  - `append()`
    - Adds an element at the end of the list
  - `clear()`
    - Removes all the elements from the list
  - `copy()`
    - Returns a copy of the list
  - `count()`
    - Returns the number of elements with the specified value
  - `extend()`
    - Add the elements of a list (or any iterable), to the end of the current list
  - `index()`
    - Returns the index of the first element with the specified value
  - `insert()`
    - Adds an element at the specified position
  - `pop()`
    - Removes the element at the specified position
  - `remove()`
    - Removes the first item with the specified value
  - `reverse()`
    - Reverses the order of the list
  - `sort()`
    - Sorts the list

* Create a List

```
thislist = ["apple", "banana", "cherry"]
print(thislist)
```

- Access element
  - Use the index within bracket notation

```
thislist = ["apple", "banana", "cherry"]
print(thislist[1])
```

- Change element

```
thislist = ["apple", "banana", "cherry"]
thislist[1] = "blackcurrant"
print(thislist)
# ['apple', 'blackcurrant', 'cherry']
```

- Add element
  - to the end of the list
    - `append()`

```
thislist = ["apple", "banana", "cherry"]
thislist.append("orange")
print(thislist)
```

    * at the specified index
        * `insert()`

```
thislist = ["apple", "banana", "cherry"]
thislist.insert(1, "orange")
print(thislist)
```

- Remove element
  - a specified item
    - `remove()`
    - only removes the first occurrence of the specified value

```
thislist = ["apple", "banana", "cherry"]
thislist.remove("banana")
print(thislist)
```

    * a specified index
    * or the last item if index is not specified
        * `pop()`

```
thislist = ["apple", "banana", "cherry"]
thislist.pop(1)
print(thislist)
```

        * `del`

```
thislist = ["apple", "banana", "cherry"]
del thislist[0]
print(thislist)
```

- Empty the list
  - `clear()`

```
thislist = ["apple", "banana", "cherry"]
thislist.clear()
print(thislist)
```

- Delete the list
  - `del`

```
thislist = ["apple", "banana", "cherry"]
del thislist
print(thislist) # "thislist" no longer exists.
```

### Tuple

- Ordered
- Immutable
  - Cannot add, change, or remove items
- Allows duplicate members

```
thistuple = ("apple", "banana", "cherry")
```

- Constructor
  - Can use the `tuple()` constructor to make a tuple

```
thistuple = tuple(("apple", "banana", "cherry"))
print(thistuple)
```

- Methods:
  - `count()`
    - Returns the number of times a specified value occurs in a tuple
  - `index()`
    - Searches the tuple for a specified value and returns the position of where it was found

* Create a Tuple

```
thistuple = ("apple", "banana", "cherry")
print(thistuple)
```

- Access element
  - Use the index within bracket notation

```
thistuple = ("apple", "banana", "cherry")
print(thistuple[1])
```

## _Objects_

### Set

- Unordered
  - The elements will appear in a random order
- Unindexed
  - Cannot access elements by index
- Iterable
- No duplicate members
- An object with no key
- Mutable\*
  - You can add or remove items
  - You cannot change items

```
thisset = {"apple", "banana", "cherry"}
```

- Constructor
  - Can use the `set()` constructor to make a set

```
thisset = set(("apple", "banana", "cherry"))
```

- Methods:
  - `add()`
    - Adds an element to the set
  - `clear()`
    - Removes all the elements from the set
  - `copy()`
    - Returns a copy of the set
  - `difference()`
    - Returns a set containing the difference between two or more sets
  - `difference_update()`
    - Removes the items in this set that are also included in another, specified set
  - `discard()`
    - Remove the specified item
  - `intersection()`
    - Returns a set, that is the intersection of two other sets
  - `intersection_update()`
    - Removes the items in this set that are not present in other, specified set(s)
  - `isdisjoint()`
    - Returns whether two sets have a intersection or not
  - `issubset()`
    - Returns whether another set contains this set or not
  - `issuperset()`
    - Returns whether this set contains another set or not
  - `pop()`
    - Removes the specified element
  - `remove()`
    - Removes the specified element
  - `symmetric_difference()`
    - Returns a set with the symmetric differences of two sets
  - `symmetric_difference_update()`
    - Inserts the symmetric differences from this set and another
  - `union()`
    - Return a set containing the union of sets
  - `update()`
    - Update the set with the union of this set and others

* Add elements
  - add one item
    - `add()`

```
thisset = {"apple", "banana", "cherry"}
thisset.add("orange")
print(thisset)
```

    * add more than one item
        * `update()`

```
thisset = {"apple", "banana", "cherry"}
thisset.update(["orange", "mango", "grapes"])
print(thisset)
```

- Remove element
  - a specified item
    - `remove()`
    - If the item to remove does not exist, it will raise an error

```
thisset = {"apple", "banana", "cherry"}
thisset.remove("banana")
print(thisset)
```

        * `discard()`
        * If the item to remove does not exist, it will NOT raise an error

```
thisset = {"apple", "banana", "cherry"}
thisset.discard("banana")
print(thisset)
```

    * a random last item
        * `pop()`

```
thisset = {"apple", "banana", "cherry"}
x = thisset.pop()
print(x)
print(thisset)
```

- Empty the set
  - `clear()`

```
thisset = {"apple", "banana", "cherry"}
thisset.clear()
print(thisset)
```

- Delete the set
  - `del`

```
thisset = {"apple", "banana", "cherry"}
del thisset
print(thisset)
```

### Dictionary

- Unordered
- Mutable
- Indexed
- No duplicate members
- Has keys and values

```
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
```

- Constructor
  - Can use the `dict()` constructor to make a dictionary
  - Keys are not string literals
  - Use equals rather than colon for the assignment

```
thisdict = dict(brand="Ford", model="Mustang", year=1964)
```

- Methods:
  - `clear()`
    - Removes all the elements from the dictionary
  - `copy()`
    - Returns a copy of the dictionary
  - `fromkeys()`
    - Returns a dictionary with the specified keys and values
  - `get()`
    - Returns the value of the specified key
  - `items()`
    - Returns a list containing the a tuple for each key value pair
  - `keys()`
    - Returns a list containing the dictionary's keys
  - `pop()`
    - Removes the element with the specified key
  - `popitem()`
    - Removes the last inserted key-value pair
  - `setdefault()`
    - Returns the value of the specified key
    - If the key does not exist: insert the key, with the specified value
  - `update()`
    - Updates the dictionary with the specified key-value pairs
  - `values()`
    - Returns a list of all the values in the dictionary

* Access property
  - Get the value of a key
    - use the key within bracket notation

```
x = thisdict["model"]
```

    * `get()`

```
x = thisdict.get("model")
```

- Change value
  - use the key within bracket notation

```
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict["year"] = 2018
```

- Add property
  - Use a new index key and assign a value to it

```
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict["color"] = "red"
print(thisdict)
```

- Remove property
  - remove a property with the specified key name
    - `del`

```
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
del thisdict["model"]
print(thisdict)
```

        * `pop()`

```
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict.pop("model")
print(thisdict)
```

    * remove the last inserted item
        * `popitem()`
        * in versions before 3.7
        * a random item is removed instead

```
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict.popitem()
print(thisdict)
```

- Empty the dictionary
  - `clear()`

```
thisset = {"apple", "banana", "cherry"}
thisset.clear()
print(thisset)
```

- Delete the dictionary
  - `del`

```
thisset = {"apple", "banana", "cherry"}
del thisset
print(thisset)
```

---

# _Iterators_

- Iterates over a list, tuple, dictionary, set, or string

## For loops

- Used for iterating over a sequence

```
mytuple = ("apple", "banana", "cherry")
for x in mytuple:
  print(x)
```

- `break`
  - Stop the loop before it has looped through all the items

```
fruits = ["apple", "banana", "cherry"]
for x in fruits:
  print(x)
  if x == "banana":
    break
```

- `continue`
  - Stop the current iteration of the loop, and continue with the next

```
fruits = ["apple", "banana", "cherry"]
for x in fruits:
  if x == "banana":
    continue
  print(x)
```

### Tuple

- You can loop through items by using a `for` loop

```
thistuple = ("apple", "banana", "cherry")
for x in thistuple:
  print(x)
```

### Sets

- You can loop through items by using a `for` loop

```
thisset = {"apple", "banana", "cherry"}
for x in thisset:
  print(x)
```

### Dictionary

- You can loop through a dictionary by using a `for` loop
- The return value are the keys of the dictionary, but there are methods to return the values as well

* Print all keys, one by one

```
for x in thisdict:
  print(x)
```

Print all values in the dictionary, one by one:

- Print all values, one by one:

```
for x in thisdict:
  print(thisdict[x])
```

    * You can also use `values()` to return values

```
for x in thisdict.values():
  print(x)
```

- Loop through both keys and values using `items()`

```
for x, y in thisdict.items():
  print(x, y)
```

## While Loops

- Execute a set of statements as long as a condition is true
- Remember to increment `i`, or else the loop will continue forever

```
i = 1
while i < 6:
  print(i)
  i += 1
```

- `break`
  - Stop the loop even if the while condition is true

```
i = 1
while i < 6:
  print(i)
  if i == 3:
    break
  i += 1
```

- `continue`
  - Stop the current iteration, and continue with the next

```
i = 0
while i < 6:
  i += 1
  if i == 3:
    continue
  print(i)
```

## Range

- `range()`
- Loops through a set of code a specified number of times
- Returns a sequence of numbers, starting from 0 (default), and increments by 1 (default), and ends at a specified number
- Loops through a range of numbers
- Defaults to 0 as a starting value
- Defaults to increment the sequence by 1

```
for x in range(6):
  print(x)
# 0, 1, 2, 3, 4, 5
```

```
for x in range(len(word)):
  print word[x]
```

- Specify the starting value by adding a second parameter
  - `range(2, 6)`
  - returns values from 2 to 6 (but not including 6)
- Specify the increment value by adding a third parameter
  - `range(2, 30, 3)`
- `for i in range(10)` in Python is the same as writing `for (var i = 0; i < 10; i++)` in JavaScript

## Else...in For loop

- The `else` keyword in a `for` loop specifies a block of code to be executed when the loop is finished

```
for x in range(6):
  print(x)
else:
  print("Finally finished!")
```

## Nested Loop

- A loop inside a loop
- The "inner loop" will be executed one time for each iteration of the "outer loop"

```
adj = ["red", "big", "tasty"]
fruits = ["apple", "banana", "cherry"]

for x in adj:
  for y in fruits:
    print(x, y)
```

## Recursion

- A defined function can call itself

```
def tri_recursion(k):
  if(k>0):
    result = k+tri_recursion(k-1)
    print(result)
  else:
    result = 0
  return result

print("\n\nRecursion Example Results")
tri_recursion(6)
```

## Create an Iterator

- Technically, in Python, an iterator is an object which implements the iterator protocol, which consist of the methods `__iter__()` and `__next__()`
- All these objects have a `iter()` method which is used to get an iterator

```
mytuple = ("apple", "banana", "cherry")
myit = iter(mytuple)

print(next(myit))
print(next(myit))
print(next(myit))
```

---

# _Conditionals_

## if

- Written by using the `if` keyword

```
a = 33
b = 200
if b > a:
  print("b is greater than a")
```

- One line if statement

```
if a > b: print("a is greater than b")
```

## elif

- If the previous conditions were not true, then try this condition

```
a = 33
b = 33
if b > a:
  print("b is greater than a")
elif a == b:
  print("a and b are equal")
```

## else

- Catches anything which isn't caught by the preceding conditions

```
a = 200
b = 33
if b > a:
  print("b is greater than a")
elif a == b:
  print("a and b are equal")
else:
  print("a is greater than b")
```

- One line if else statement

```
print("A") if a > b else print("B")
```

---

# _Try Except_

- `try`
  - Tests a block of code for errors
- `except`
  - Handles the error
- `finally`
  - Executes code, regardless of the result of the `try` and `except` blocks
- Can use the `else` keyword to define a block of code to be executed if no errors were raised

```
try:
  print(x)
except:
  print("Something went wrong")
else:
  print("Nothing went wrong")
finally:
  print("The 'try except else' is finished")
```

---

# _Modules_

- A file containing a set of functions you want to include in your application

- When using a function from a module, use the syntax: `module_name.function_name`
  - `mymodule.py`

```
def greeting(name):
  print("Hello, " + name)
```

    * `index.py`

```
import mymodule

mymodule.greeting("Chase")
```

- Importing from a parent folder

```
import sys
sys.path.append('..')
import filename
```

- Importing from a different folder

```
import os
import sys
sys.path.insert(1, os.path.join(sys.path[0], '..'))
import filename
```

- Alias

```
import mymodule as mm

a = mm.greeting("Chase")
print(a)
```

- `from`
  - Import only parts from a module

```
from mymodule import greeting

print (greeting("Chase"))
```

- `dir()`
  - Lists all the function and variable names in a module

```
import mymodule

x = dir(mymodule)
print(x)
```

---

# _Built-in Modules_

- platform
  - ` import``` `platform`
  - `platform.system()`
- datetime
  - ` import``` `datetime`
  - `datetime.datetime.now()`
    - displays the current date
- json
  - ` import``` `json`
  - `json.loads()`
    - parse JSON to Python object
  - `json.dumps()`
    - parse Python object to JSON
- sha
  - `import sha`
  - provides access to the SHA-1 message digest algorithm
  - `sha.sha("hello").hexdigest()`
    - generates a hex digest
- pickle
  - `import pickle`
  - serializes and deserializes data for easy transport
  - `pickle.dumps(data)`
  - `pickle.loads(serialized_data)`
- os
  - `import os`
  - `os.path.isfile('filename')`
- ecdsa
  - `from ecdsa import SigningKey, SECP256k1`
-

---

# _Sockets_

You can loop through a dictionary by using a for loop.

---

# _Built-in Functions_

- https://www.w3schools.com/python/python_ref_functions.asp

- `abs()`
  - Returns the absolute value of a number
- `all()`
  - Returns True if all items in an iterable object are true
- `any()`
  - Returns True if any item in an iterable object is true
- `ascii()`
  - Returns a readable version of an object. Replaces none-ascii characters with escape character
- `bin()`
  - Returns the binary version of a number
- `bool()`
  - Returns the boolean value of the specified object
- `bytearray()`
  - Returns an array of bytes
- `bytes()`
  - Returns a bytes object
- `callable()`
  - Returns True if the specified object is callable, otherwise False
- `chr()`
  - Returns a character from the specified Unicode code.
- `classmethod()`
  - Converts a method into a class method
- `compile()`
  - Returns the specified source as an object, ready to be executed
- `complex()`
  - Returns a complex number
- `delattr()`
  - Deletes the specified attribute (property or method) from the specified object
- `dict()`
  - Returns a dictionary (Array)
- `dir()`
  - Returns a list of the specified object's properties and methods
- `divmod()`
  - Returns the quotient and the remainder when argument1 is divided by argument2
- `enumerate()`
  - Takes a collection (e.g. a tuple) and returns it as an enumerate object
- `eval()`
  - Evaluates and executes an expression
- `exec()`
  - Executes the specified code (or object)
- `filter()`
  - Use a filter function to exclude items in an iterable object
- `float()`
  - Returns a floating point number
- `format()`
  - Formats a specified value
- `frozenset()`
  - Returns a frozenset object
- `getattr()`
  - Returns the value of the specified attribute (property or method)
- `globals()`
  - Returns the current global symbol table as a dictionary
- `hasattr()`
  - Returns True if the specified object has the specified attribute (property/method)
- `hash()`
  - Returns the hash value of a specified object
- `help()`
  - Executes the built-in help system
  - Returns the built-in documentation metadata associated with an object
    - known as the docstring

```
help("a string".join)
Help on built-in function join:
<BLANKLINE>
join(...)
    S.join(sequence) -> string
<BLANKLINE>
    Return a string which is the concatenation of the strings in the
    sequence.  The separator between elements is S.
<BLANKLINE>
```

- `hex()`
  - Converts a number into a hexadecimal value
- `id()`
  - Returns the id of an object
- `input()`
  - Allowing user input
- `int()`
  - Returns an integer number
- `isinstance()`
  - Returns True if a specified object is an instance of a specified object
- `issubclass()`
  - Returns True if a specified class is a subclass of a specified object
- `iter()`
  - Returns an iterator object
- `len()`
  - Returns the number of items in an object
  - For Lists, Tuples, Sets, Dictionary, Strings
- `locals()`
  - Returns an updated dictionary of the current local symbol table
- `map()`
  - Returns the specified iterator with the specified function applied to each item
- `max()`
  - Returns the largest item in an iterable
- `memoryview()`
  - Returns a memory view object
- `min()`
  - Returns the smallest item in an iterable
- `next()`
  - Returns the next item in an iterable
- `object()`
  - Returns a new object
- `oct()`
  - Converts a number into an octal
- `open()`
  - Opens a file and returns a file object
- `ord()`
  - Convert an integer representing the Unicode of the specified character
- `pow()`
  - Returns the value of x to the power of y
- `property()`
  - Gets, sets, deletes a property
- `range()`
  - Returns a sequence of numbers, starting from 0 and increments by 1 (by default)
- `repr()`
  - Returns a readable version of an object
- `reversed()`
  - Returns a reversed iterator
- `round()`
  - Rounds a numbers
- `setattr()`
  - Sets an attribute (property/method) of an object
- `slice()`
  - Returns a slice object
- `sorted()`
  - Returns a sorted list
- `@staticmethod()`
  - Converts a method into a static method
- `str()`
  - Returns a string object
- `sum()`
  - Sums the items of an iterator
- `type()`
  - Returns the type of an object
- `vars()`
  - Returns the **dict** property of an object
- `zip()`
  - Returns an iterator, from two or more iterators

---

# _Syntax_

## Naming

- Functions and variables use `joined_lower` casing
- Classes use `StudlyCaps`

## Code blocks

- Python relies on indentation, using whitespace, to define scope in the code
- Indent using 2 spaces

```
if 5 > 2:
  print("Five is greater than two!")
```

## Comments

```
# This is a comment.
```

## Lambdas

```
lambda a: a * 2
```

## Destructuring

```
status, data = getResult()
```

```
numbers = (1, 2, 3)
x, y, z = numbers
```

## Spread operator

```
search_db(**parameters)
```

```
import datetime
date_fields = (2017, 12, 4)
date = datetime.date(*date_fields)

numbers = [1, 2, 3, 4]
first, *remaining = numbers

first = [1, 2]
second = [3, 4]
combined = first + second
```

## Iterators

### While

```
def fibonacci():
    pre, cur = 0, 1
    while True:
        pre, cur = cur, pre + cur
        yield cur
```

### For In

```
for x in fibonacci():
    if (x > 1000):
        break
    print x,
```

## Classes

```
class SpiderMan(Human, SuperHero):
    def __init__(self, age):
        super(SpiderMan, self).__init__(age)
        self.age = age
    def attack(self):
        print 'launch web'
```

```
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    def __str__(self):
        return f"({self.x}, {self.y})"
```

## Sub Class (extend)

```
class ColorPoint(Point):
    def __init__(self, x, y, color):
        super().__init__(x, y)
        self.color = color
    def __str__(self):
        return "{} in color {}".format(super().__str__(), self.color)
```

## Map

```
map(lambda: x*2, [1,2,3,4])
```

## Length

```
len([])
```

## Generators

```
def foo():
    yield 1
    yield 2
    yield 3
```

## Range

```
print range(5)
# 0, 1, 2, 3, 4
```

## Imports

```
import math
print(math.log(42))

from math import log
print(log(42))

# not a good practice (pollutes local scope)
from math import *
print(log(42))
```

## Expression Interpolation (template literal)

```
a = 5
b = 10
print(f'Fifteen is {a + b} and not {2 * a + b}.')
```

```
d = {"name" : "bob", "money" : 5}
"Hello %(name)s, I need %(money)d dollars." % d
# 'Hello bob, I need 5 dollars.'
```

## Arrow function

```
`numbers = [1, 2, 3, 4]list(map(lambda x: x * 2, numbers))
# or [x * 2 for x in numbers]`
```

## Default Parameter

```
`def multiply(a, b=1):return a * b`
```

## Rest Parameter

```
from functools import reduce
def product(*numbers):
    return reduce(lambda x, y: x * y, numbers)

print(product(1, 2, 3, 4))
```

## Getter & Setter

```
class SmartPoint(Point):
    @property
    def hypotenuse(self):
        return sqrt(self.x ** 2 + self.y ** 2)

    @hypotenuse.setter
    def hypotenuse(self, z):
        self.y = sqrt(z ** 2 - self.x ** 2)
```

## Async/Await

```
async def getProcessedData(url):
    try:
        v = await downloadData(url)
    except Exception:
        v = await downloadFallbackData(url)
    await processDataInWorker(v)
```

## Docstrings (multi-line strings)

```
`print("""string text line 1
string text line 2""")|`
```

---

# _Language Conversion_

## JavaScript compilers

- Transcrypt
  - http://www.transcrypt.org/home
  - `python -m pip install transcrypt`
  - To Use:
    - `transcrypt filename.py`

## JavaScript translators

- Brython
  - Python → Javascript
  - https://www.brython.info/tests/editor.html?lang=en
- javascripthon
  - Best one
  - Python 3 → ES6 Javascript
  - https://github.com/metapensiero/metapensiero.pj
  - `pip install javascripthon`
  - To Use:
    - `python -m metapensiero.pj mysourcefile.py`
- pyjs
  - Dead project
  - http://pyjs.org/
- jiphy
  - Dead project
  - https://github.com/timothycrosley/jiphy
  - `pip install jiphy`
  - Doesn't support ES6
  - To Use:
    - `jiphy mypythonfile.py`

---

# _React_

## python-react

- To install `python-react`, use pip like so:
  - `bash pip install react`
- You can now render React code with a Python app by providing the path to your `.jsx` components and serving the app with a render server. Usually this is a separate `Node.js` process
- To run a render server, follow this [easy short guide](https://github.com/markfinger/python-react/tree/master/examples/basic_rendering).
- Now you can start your server as so:
  - `bash node render_server.js`
- Start your python application:
  - `bash python app.py`
- And load up http://127.0.0.1:5000 in a browser to see your React code rendering

* Django
  - Add `react` to your `INSTALLED_APPS` and provide some configuration as so:

```
bash INSTALLED_APPS = ( # … ‘react’, )
REACT = { ‘RENDER’: not DEBUG, ‘RENDER_URL’: ‘http://127.0.0.1:8001/render’, }
```

## PyReact

- https://github.com/doconix/pyreact

---

# _Misc_

- Differences between JavaScript and Python
  - https://blog.glyphobet.net/essay/2557/

* nodemon works for Python files
  - `nodemon hello.py`

## VSCode

- https://ruddra.com/2017/08/19/vs-code-for-python-development/

---

---
layout: proj
title: Beginners Python Tutorial
---
# Beginners Python Tutorial

<hr>

This was my first talk and I can still recollect the day experience, I was waiting for my name to be called upon and at the same time my legs was shivering like it doesn't in winter. On other hand my face was covered with sweat. I was trying to squeeze my hand as hard as I can, it was my trick to overcome stage fear.

While my brain was busy fighting with fear, involuntry movement was still in progress, I heard my name. I walked on the stage, I can only see more than 100 bobble heads. For second, I stopped and taken a deep breath and started the talk.


### WHY Python?
* Ever imagined that your pseudo code can be your actual working code. Welcome to Python!
* If you consider pointers(*) is too archaic as well as your biggest enemy.
* Interpreter based, bug can be found easily. At the same time, it lead to create more bugs.
* Prebuilt highly optimized datastructure i.e. tuple, list and dictionary.
* [Zen of Python](https://www.python.org/dev/peps/pep-0020/) by Tim Peters.

### Compiler Vs Interpreter

<figure>
  <div class="large ">
    <img src="{{ site.url }}/assets/images/projects/others/talks/comp-vs-inter.png" alt="system design">
    <figcaption>Fig1.1 Compiler vs Interpreter </figcaption>
  </div>
</figure>

* Source Code: This is the input for any programming language.
* Checker: It confirms the syntax, static semantic correct or not.
* Compiler: It converts sequences in further low level intruction.
* Object Code: It is the low level intruction file.
* Interpreter: It follows the sequences of simple instruction given.
* Output: final result.

For an interpreted language, there's a special program that converts that source code to an internal data structure and then sequentially converts each step into a low machine instructions and executions.

### Python Setup
Now days most of the OSes comes with Python but still if you don't have it. Download it from [here](https://www.python.org/downloads/).

Once you have install, open your default shell and type `python`. You will see prompt like below

```python
rahul@localhost: python
Python 2.7.1 (default, Jun 20 2012, 14:05:02)
[GCC 4.2.1 Compatible Apple LLVM 7.3.0 (clang-703.0.31)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> print("Hello, World!")
Hello, World!
```
Once setup is done, now we are ready to write Python programs for solving problem available in our universe.

### Diving into code
At heart, every programs will manipulate data objects and each object has a type that defines the kinds of things programs can do to it


Objects are:

 * Scalar (i.e. cannot be subdivided) Example: int, float, bool etc
 * Non-scalar (i.e. have internal structure that can be accessed or set of scalar elements) Example: List, String, Class etc

### TYPE
You can use built in Python function type returns the type of an object.

```python
>>> type(3)
<type ‘int’>
>>> type(3.o)
<type ‘float’>
>>> type([1, 2, 4])
<type 'list'>
```

#### Type Conversion

Python allows to convert a object from one built in [type](https://en.wikipedia.org/wiki/Data_type) to another one.

```python
>>> a = int("34")
>>> a
34
>>> b = float("3.1415926")
>>> b
3.1415926
>>> int('a')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: invalid literal for int() with base 10: 'a'
>>> "Task 1: Read the above error message and figure out why it is happening?"
```

###  EXPRESSION
Objects and operators can be combined to form expressions, each of which denotes an object of some type. The syntax for most simple expressions is: –

```
<object> <operator> <object>
```

Example,

```python
>>> 3 + 5
8
>>> 3.14 * 20
62.8
>>> (2 + 3) * 4
20
>>> 2 + 3 * 4
14
```
You can read more about operator precedence [here](https://docs.python.org/3/reference/expressions.html#operator-precedence).

### Comparison Operator
Unlike C, all comparison operations in Python have the same priority, which is lower than that of any arithmetic, shifting or bitwise operation. Also unlike C, [expressions](https://docs.python.org/2/reference/expressions.html) like `a < b < c` have the interpretation that is conventional in mathematics:

Operators  |  "<" | ">" | "==" | ">=" | "<=" | "!=" | "is" ["not"] | ["not"] "in"

#### Some use cases

```python
>>> 10 == 12
False
>>> 'i' in 'indigo' # It looks if `i` present in `indigo`
True
>>> 5 is not 4
True
>>> 5 <= 2
False
```
Comparisons yield boolean values: True or False.

### String
We all know how important String is in our life. Python String comes with complete diamond package. It have all the improtant methods you will need on String manipulation.

```python
# lets apply some basic operators
>>> 3 * 'a'
'aaa'
>>> 'a' + 'a'
'aa'
>>> 'a' + str(4)
'a4'
>>> len('abc')
3

# Now time for some string methods
>>> 'abc'.capitalize() # convert to uppercase
'ABC'
>>> "The sum of 1 + 2 is {0}".format(1+2) # format is like placeholder. You can do a lot of customization with it.
'The sum of 1 + 2 is 3'

>>> 'abc'.find('b')  # returns the index of the element
1
>>> '1,2,3'.split(',') # returns a list of words in string, using sep as deliminator
['1', '2', '3']

# Sequence type operation
>>> 'abc'[0] # return the 1st element
'a'
>>> 'abc'[2] # return the 3rd element
'c'
>>>
```

* Tip: `str` and `len` are built in python method which are always available. The more you become proficient with [these method](https://docs.python.org/3/library/functions.html), the better pythonista you will be.

For detail reading about String type you can always heads to [official documentation](https://docs.python.org/3.4/library/string.html).

### Sequence Type
"Sequence" is not an object, it is more like an informal interface or protocol for some objects like list which implements it. If a type is sequences it provides access to various handy operation. For Example, random access, slicing etc.

x in s | True if an item of s is equal to x, else False
x not in s | False if an item of s is equal to x, else True
s + t | the concatenation of s and t
s * n or n * s | equivalent to adding s to itself n times
s[i]  | ith item of s, origin 0
s[i:j] | slice of s from i to j
s[i:j:k]  | slice of s from i to j with step k
len(s) | length of s
min(s) | smallest item of s
max(s) | largest item of s
s.index(x[, i[, j]]) | index of the first occurrence of x in s (at or after index i and before index j)
s.count(x) | total number of occurrences of x in s

#### See it in action
```python
>>> 'a' in 'abc'
True
>>> 'a' not in 'abc'
False
>>> 'a' + '2'
'a2'
>>> 'a' * 5
'aaaaa'
>>> 'abc'[0]
'a'
>>> 'abc'[0:2]
'ab'
>>> 'abc'[0:3:1]
'abc'
>>> 'abc'[0:3:2]
'ac'
>>> len('abc')
3
>>> min('abc')
'a'
>>> max('abc')
'c'
>>> 'abc'.index('b', 0, 3)
1
>>> 'abc'.count('c')
1
```

These are handy operations, so which types implements sequence.

* List, Tuple and Range

Apart from these [binary data(https://docs.python.org/3.4/library/stdtypes.html#binaryseq) and [text strings](https://docs.python.org/3.4/library/stdtypes.html#textseq) also implements tailored version of it. Now, you must be able to figure out why we were able to apply random access on String?


### More of Sequence Type

There are two types of sequence:
* Immutable: This sequence is implemented by data structure whose value cannot be modified after the assignemnt. The only operation that immutable sequence types generally implement which is not in immutable is support for built in `hash()`. Example: Tuple
* Mutable: The valued contained can be changed. Example: List, Dictionary

Apart from above mentioned operations, follwing few more are also implemented by below data structures.

del s[i:j] | same as s[i:j] = []
s[i:j:k] = t | the elements of s[i:j:k] are replaced by those of t
s.append(x) | appends x to the end of the sequence (same as s[len(s):len(s)] = [x])
s.clear() | removes all items from s (same as del s[:])
s.copy() | creates a shallow copy of s (same as s[:])
s.extend(t) or s += t | extends s with the contents of t (for the most part the same as s[len(s):len(s)] = t)
s *= n  | updates s with its contents repeated n times  (6)
s.insert(i, x) | inserts x into s at the index given by i (same as s[i:i] = [x])
s.pop([i]) | retrieves the item at i and also removes it from s  (2)
s.remove(x) | remove the first item from s where s[i] == x  (3)
s.reverse() | reverses the items of s in place

* Tip: Python data structure is really powerful. Getting well versed with these will help you solve moonshot problems.

#### Tuple
Tuples are immutable sequences, typically used to store collections of heterogeneous data (such as the 2-tuples produced by the enumerate() built-in).

Tuples may be constructed in a number of ways:
  * Using a pair of parentheses to denote the empty tuple: ()
  * Using a trailing comma for a singleton tuple: a, or (a,)
  * Separating items with commas: a, b, c or (a, b, c)
  * Using the tuple() built-in: tuple() or tuple(iterable)

```python
>>> t = ()
>>> t
()
>>> t = (1, 2, 3)
>>> t
(1, 2, 3)
>>> tuple('abc')
('a', 'b', 'c')
>>>
```

#### List
Lists are mutable sequences, typically used to store collections of homogeneous items.

Lists may be constructed in several ways:
  * Using a pair of square brackets to denote the empty list: []
  * Using square brackets, separating items with commas: [a], [a, b, c]
  * Using a list comprehension: [x for x in iterable]
  * Using the type constructor: list() or list(iterable)

```python
>>> l = []
>>> l
[]
>>> l = [1, 2, 3]
>>> l
[1, 2, 3]
>>> l = ['a']
>>> l
['a']
>>> [x for x in range(5)]
[0, 1, 2, 3, 4]
>>> list('abc')  # String is iterable
['a', 'b', 'c']
```

#### Ranges
The range type represents an immutable sequence of numbers and is commonly used for looping a specific number of times in for loops.

```python
>>> list(range(10))
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> list(range(1, 11))
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> list(range(0, 30, 5))
[0, 5, 10, 15, 20, 25]
>>> list(range(0, 10, 3))
[0, 3, 6, 9]
>>> list(range(0, -10, -1))
[0, -1, -2, -3, -4, -5, -6, -7, -8, -9]
>>> list(range(0))
[]
>>> list(range(1, 0))
[]
```

### Getting input from user

If we are going to write programs or scripts, we will need a way to incorporate input from a user.

```python
>>> a = raw_input()
5
>>> a  # by default raw_input converts your elements into string
'5'
>>> a = raw_input("Enter a float! ") # you can have custom message
Enter a float! 5.0
>>> a
'5.0'
```

I think at this point we have already covered about basic of python i.e. types. At this point you can take a break and have a coffee.

### Conditionals
Program has to make decision and it is  required when a program has more than one choice of actions depending on a variable's value.

<figure>
  <div class="large ">
    <img src="{{ site.url }}/assets/images/projects/others/talks/conditional.jpg" alt="system design">
  </div>
</figure>

Python provide you the decision making using conditional expressions. Let go through it by an Example.

```python
# filename: conditional.py

x = int(raw_input('Enter an integer: ')) # see type casting here

# check if number is even using % (modulo) operator
if x % 2 == 0:
    print('Even')
else:
    print('Odd')

print('Done with conditional')

# Running above python script
$ python conditional.py
Enter an integer: 5
Odd
Done with conditional
```

#### Some observation
* The expression x % 2 == 0 evaluates to False when the remainder of x divided by 2 is 1!
    * Note that == is used for comparison, since = is reserved for assignment
* The indentation is important – each indented set of expressions denotes a block of instructions
    * For example, if the last statement was indented, it would be executed as part of the else block of code
    * No more opening-closing braces tracking :)
* Note how this indentation provides a visual structure that reflects the semantic structure of the program

Read more about python indentation [here](https://www.python.org/dev/peps/pep-0008/).


#### Nested conditional
```python
# filename: nested_conditional.py

x = 6

if x % 2 == 0:
    if x % 3 == 0:
        print('Divisible by 2 and 3')
    else:
        print('Divisible by 2 and not by 3')
elif x % 3 == 0:
    print('Divisible by 3 and not by 2')

# Running the script
$ python nested_conditional.py
Divisible by 2 and 3
```

#### Compound Boolean

```python
# filename: compound_conditional.py

x = 3
y = 5
z = 7

if x < y and x < z:
  print('{0} is least'.format(x)) # see the use of format
elif y < z;
  print('{0} is least'.format(y))
else:
  print('{0} is least'.format(z))

# Running the script
$ python compound_conditional.py
3 is least
```


### Iteration
Repeated execution of a set of statements is called iteration.

<figure>
  <div class="large ">
    <img src="{{ site.url }}/assets/images/projects/others/talks/iteration.png" alt="system design">
  </div>
</figure>

In python or in general any programming langauge, looping/iteration is defined on three steps.

1. Assignment: A assignment in python makes an existing variable refer to a new value (and stop referring to the old value).
2. Condition: It is our decision maker
3. Updation: The new value of the variable depends on its old value and variable refers to the new value.

```python
for i in [1, 2, 3]:
  print(i)        # by default print have newline.
1
2
3
```

Let see some more example of iteration in python along with few problems.

#### While
A while loop statement repeatedly executes a target statement as long as a given condition is true.

```python

count = 0              # Assignment
while (count < 9):     # Condition
  count = count + 1    # Updation
  print('I am learning python for {} time'.format(count))

print "Good bye!"

# Output
I am learning python for 1 time
I am learning python for 2 time
I am learning python for 3 time
I am learning python for 4 time
I am learning python for 5 time
I am learning python for 6 time
I am learning python for 7 time
I am learning python for 8 time
I am learning python for 9 time
Good bye!
```

Want to write a program which tries to discover infinity, here goes,

```python
var = 1
while True:  # This constructs an infinite loop
   print("I am becoming one step closer to infinity!")
```

but you can stop this `break`

```python
var = 1
while True:  # This constructs an infinite loop
   print("I am becoming one step closer to infinity!")
   break
print("I stopped after 1st step")
```

#### For
For loop is used when we want to loop through a set of things such as a list of words, the lines in a file or a list of numbers.

```python
Avengers = ['Ironman', 'Captain America', 'Hulk']
for superhero in Avengers:
    print('Hello, {0}'.format(superhero))
print 'Done!'  # Remember indentation is key

# Output
Hello, Ironman
Hello, Captain America
Hello, Hulk
Done!
```
Let's sum the number from 1 to 99

```python
sum = 0
for num in range(1, 100):  # range will create the list [1, 2,...99]
    sum += num             # this line update the sum value
print 'Sum: ', sum
```

#### Nested
You can loop inside another loop.

```python
for iterating_var in sequence:
   for iterating_var in sequence:
      statements(s)
   statements(s)
```
For while

```python
while expression:
   while expression:
      statement(s)
   statement(s)
```


One more example

```python

for i in [1, 2, 3]:
  for j in [101, 102, 103]:
    print('{0}, {1}'.format(i, j))

Output:
1, 101
1, 102
1, 103
2, 101
2, 102
2, 103
3, 101
3, 102
3, 103
```

### Functions/Methods
Functions are a convenient way to divide your code into useful blocks which can be reused. For example, above we were trying to sum the elements and let suppose we need it at 100 places. Should we copy the code at 100 places in our program. No way!

Here comes the functions to help us out.

```python
# let make a sum function

def sum_integer():
  sum = 0
  for num in range(1, 100):
    sum += num
  return sum

# call this function and print the result, see the () in calling
print(sum_integer())

# Output:
4950
```

Can improve it? Currectly our sum method method always return 100. What if we want sum for first 50 numbers.

Here comes the concept of argument, function can take variable as argument.

```python
# let make a sum function

def sum_integer(last_num): # last num is the variable which will contain the value
  sum = 0
  for num in range(1, last_num):
    sum += num
  return sum

# call this function and print the result, we are passing 50 as an argument
print(sum_integer(50))

# Output:
1225
```

Moving further, I still think out sum function is kinda rigid. What if I want to sum between given two number or if I don't provide the first number it should take the default first number to 1.

Here we will use the concept of default value in argument

```python
# let make a sum function

def sum_integer(first_num=1, last_num): # first_num if didn't provided a value it will take 1 as default
  sum = 0
  for num in range(first_num, last_num):
    sum += num
  return sum

# call this function and print the result, we are passing 50 as an argument
print(sum_integer(50))
print(sum_integer(25, 100))

# Output:
1225
925
```

Talk ends here.




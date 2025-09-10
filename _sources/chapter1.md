# Part I Introduction to Coding Concepts Using Python

## Chapter 1 Using Python Interactively
Python is a very versatile language that includes a lot of built-in functionality, as well as many  add-ons. Python code is interpreted, which means that it is executed one line at a time. There  are several environments in which Python can be used. The main ones are the Python  interpreters, creation of scripts, and Jupyter notebooks.

- The Python interpreters allow you to enter and execute code one line at a time. • Scripts allow you to save multiple lines of code in a file and then execute them  sequentially, which gives the results all at once rather than executing and getting the  results one line at a time. To create a script, use an editor and save a file with an  extension of .py on the filename.
- Jupyter notebooks allow combinations of text that can be formatted and executable  code (and the results) in one document; the code is entered in cells.

The details of installation and implementation will not be covered in this book, but it is  assumed that the reader will have access to some form of Python and will be able to follow  along and test the code. This book uses Python 3, which is quite different from Python 2.

Since Python is interpreted, it is possible to use Python interactively. This means that you (the  user) enter an expression, and then Python responds with the result. What this looks like  depends on the environment in which you are using Python.
In some cases, such as using the Python interpreter, you will see a prompt, which is generally  three greater than signs in a row, e.g.,

`>>>`

When you see this prompt, you can enter an expression, e.g. 3 + 5, and then hit the Return key.

```python
>>> 3 + 5
8
>>>
```

The Python interpreter responds with the result (in this case, 8), and then displays another  prompt so that you can enter another expression. Note that this is the prompt for a one-line  expression. When code takes multiple lines, the >>> is the first or primary prompt. This is  followed by lines starting with an ellipsis, which is 3 dots in a row (...), which is called the  secondary prompt.

In some cases, such as in Jupyter notebooks or ipython, the prompt will be the word “In” and  then an integer in square brackets followed by a colon, and the response will consist of the  word “Out” and then the same integer in square brackets with a colon, e.g.

```python
In[1]: 3 + 5
Out[1]: 8
```

The integers increase sequentially as you enter and execute expressions.

Some environments, such as Jupyter notebooks, allow more than one expression to be entered  into a cell, and then executed sequentially together.

In this text, although the actual prompt looks different in different environments, the prompt(s)  will be shown as >>>. The prompt and the user input will be shown in a code font in italics, and  the Python response will not have italics, e.g.

```python
>>> 3 + 5
8
```

In order to be concise, the prompt that would appear after the result will not be shown.

Note that the prompt will be shown for short, simple codes. Longer code will instead be shown  in boxes.

All expressions (for now) should begin in the first column; they should not be indented. Spacing  and indentation is important in Python; following this rule will avoid some errors.
Longer expressions can be extended to another line by either putting a `\` at the end of the first  line, or putting the expression in parentheses. This can be extended to multiple lines, also.

```python
>>> 1 + 2 + 3 + \
...4 + 5
15
>>> (1 + 2 + 3
...+ 4 + 5)
15
```

Using parentheses is generally preferred. In these examples, the addition operator (+) can be at  the end of one line, or at the beginning of the next, as shown. Also, note the primary prompt  >>> on the first line, and the secondary prompt … on the second line of these examples.

### 1.1 Variables and Assignment Statements

If it is desired to store a value for subsequent use, a variable can be used. Values can be stored  in variables using an assignment statement. The general form of an assignment statement is

```python
variable = expression
```

where the name of the variable is on the left, the assignment operator is the single equal sign,  and the expression is on the right. For simplicity we can assume that the way it works is that  first the expression is evaluated, and then the value of the expression is assigned to the  variable. For example, the statement

```python
>>> mynumber = 29 + 4
```

stores the number 33 in the variable called `mynumber`. This result is not displayed by default.  However, just typing the name of a variable at the prompt will display the value, e.g.

```python
>>> mynumber
33
```

The terminology is that the assignment binds the variable name `mynumber` to the value 33. The  33 is stored in a location, and the variable `mynumber` references that location.

As we will see later, what we are calling variables here are actually objects. While a variable  simply stores a value, an object has both attributes such as the data stored in it, as well as  functions that can operate on the data (these are called methods). For now, however, we will  keep it simple and refer to them as variables.

Values of some types of variables can change. Types that can change are called mutable, and  types that cannot change are immutable. Number variables are immutable types. When the  variable `mynumber` is used or displayed, it refers to the value that is stored in it. The following  will take the current value of the variable `mynumber` (which is 33), subtract 2 from it, to result  in the number 31, which is stored in a new location. The assignment binds the variable `mynumber` to this new location. It appears as though the value of `mynumber` has changed, and  it is easiest to think of it that way. In reality, `mynumber` now refers to a new location in which  31 is stored.

```python
>>> mynumber = mynumber – 2
>>> mynumber
31
```

This demonstrates that the order of operations in an assignment statement is important: first  the expression on the right is evaluated, and then the result is stored in a location that is bound  to the variable on the left (which may or may not be the same variable). This means that the  equal sign, which is the assignment operator, does NOT mean equality! One way to read this  out loud, instead of using the word “equals”, is to say “`mynumber` gets the value of `mynumber` minus 2”.

Adding a value to a variable is called incrementing the variable, and subtracting from it is called  decrementing.

There are rules for variable names: they must start with a letter of the alphabet or the  underscore character (_), and then can have any combination of letters, digits, and the  underscore character. Spaces may not be used in variable names. It is common to use all lower  case letters. Variable names should be mnemonic, which means that the name should help to  explain what is stored in the variable. For example, to store the radius of a circle in a variable,  the variable name radius would be mnemonic; a variable called x would not be descriptive.

Python also has a default variable, which is just the underscore character. Whenever an  expression is entered interactively, and the result is not stored in a variable, Python stores it in  the default variable _. This variable is reused every time just an expression is entered. For  example,

```python
>>> 3 + 5
8
>>> _ + 4
12
>>> _ * 2
24
```

It is best practice, however, to avoid using this default variable.

Multiple assignments can be made in one statement, e.g.

```python
>>> a, b = 5, 33
```

This will assign the value of 5 to the variable a and the value of 33 to the variable b. It is easier  to read code in which every assignment is on a separate line, however, so this usage is generally  discouraged. An exception might be assigning 0’s to several variables at once, and we will see  later that there are some interesting applications for this simultaneous assignment.
The word ‘variable’ means something that can change, and that is how variables are used in  coding. Constants are values that cannot change during the execution of the code. Some  languages provide a way to define constants, but Python does not. Instead, a value that is  meant to be a constant in Python code is by convention stored in a variable named with all  upper-case letters. For example, a tax rate might be defined in an assignment statement as  follows.

```python
>>> TAX_RATE = 0.05
```

To delete any variable that has been created, use the del statement:

```python
>>> del mynumber
```

### 1.2 Built-in Functions

Python has many built-in functions that can be used. As an example of a built-in function, we  will first examine the round function. An example of using it is:

```python
>>> round(7.6)
8
```

This rounds the real number 7.6 up to the integer 8.

The terminology when using a function is that the function is called; the function call includes  the name of the function and argument(s) that are passed to it in parentheses. If there are multiple arguments, they are separated by commas. In this example, the argument 7.6 was  passed to the function named round. Most functions return a result; in this case, the rounded  result of 8 is returned.

Another, different type of function is the print function. For example, the value stored in a  variable can be displayed using the print function, as in:

```python
>>> val = 5 * 2
>>> print(val)
10
```

Of course, the value of the variable can also be displayed by just typing the name of the  variable. The print function, however, can be used to display more than one result, e.g.

```python
>>> print(val, 2*3)
10 6
```

Note that a space is automatically printed between the two values.

With the print function, the values of the expression arguments are displayed, and it might not  seem like any result is returned. The print function, however, actually returns the special value  None, since it does not really need to return anything. Normally this value is not seen or used,  but can be displayed by assigning the result of calling the print function to a variable (which is  not something that would typically be done!). We will see that all Python functions return  something (even if it is just None, as with print).

Names of functions should never be used as variable names. Although it is technically possible  to do this, it would eliminate the use of the function itself (at least temporarily, until the  variable is deleted). For example, if the word ‘print’ is used as a variable, it could not then be  used to print anything. The second statement here would create an error message because  print is now a variable, not a function that can be called.

```python
>>> print = 11
>>> print(8-3)
TypeError: 'int' object is not callable
```

Note that the actual error message may be different in the various Python programming  environments.

Deleting the print variable would, however, restore the use of the print function:

```python
>>> del print
>>> print(8-3)
5
```

### 1.3 Types and Operators

There are several built-in types for expressions and variables. Each type has different operators  and functions that can be used with expressions of that type.

Variables in Python are actually objects, which are created from classes. We will see more on  objects and object oriented programming (OOP) in a later chapter.

#### 1.3.1 Numbers

Simple numbers can be integers (whole numbers, with no decimal point), or real numbers  (which have a decimal point). Integers are of the type int in Python, and real numbers are of the type float. There are also complex numbers, which are of the type complex (and are in the  form a + bj or a+bJ). The type of an expression can be determined using the type function. For  example,

```python
>>> print(type(1+3), type(5.2))
<class 'int'> <class 'float'>
```

Python shows that the type (or class) of the first expression is int, whereas the type of 5.2 is  float.

Numbers can be written in scientific notation using “e”, as in 2e3, which is equivalent to 2*103.  The result is always a float.

```python
>>> 2e3
2000.0
```

There are operators and functions that work with numbers.

We have seen some basic math operators, which include:

```python
Addition +
Subtraction -
Multiplication *
Negation -
```

The addition, subtraction, and multiplication operators are called binary operators, as they  operate on two operands. Negation is a unary operator, as it operates on only one operand.
When using these operators, if the operand(s) are integers, the result will be an integer (type  int). If anything in the expression is a float, however, the result will be a float.

```python
>>> 3 + 5
8
>>> 5.2 – 3.2
2.0
```

Other operators include:

```python
Exponentiation **
Float division /
Integer division //
Remainder division %
```

Exponentiation, or raising one number to a power, is accomplished using the ** operator. For  example, 5 ** 2 is 52, which is 5 raised to the second power, or 5 squared, or 25.

```python
>>> 5 ** 2
25
```

There are several division operators.

The / division operator always results in a float, regardless of the types of the operands. For  example,

```python
>>> 5.2/2
2.6
>>> 6/3
2.0
```

The // division operator always results in an integer (conceptually, anyway!), regardless of the  types of the operands. The // operator results in the whole number part of the division, and is  sometimes called floor division since it gets rid of the fractional part. The following examples  show that 2 divides into 7 three times, 4 divides into 7 once, and 3 divides into 7.5 two times.

```python
>>> 7//2
3
>>> 7//4
1
>>> 7.5//3
2.0
```

Notice the types of the results. With the expression 7.5//3, the result that is returned is  conceptually the integer 2, but it is stored as a float and not the type int since the expression  contains a float.

The % operator will show the remainder (or modulus) of these divisions, e.g.

```python
>>> 7.5%3
1.5
>>> 7%4
3
```

So, 3 goes into 7.5 two times, with a remainder of 1.5 (7.5-3*2), and 4 goes into 7 one time with  a remainder of 3. Again, notice the types of the results.

In addition to the built-in operators, there are math functions that are in core Python. These  include rounding functions such as round, which we have already seen:

```python
>>> round(7.5)
8
```

The round function can also round floats to a specified number of decimal places. For example,  we can round 8/3 to 2 decimal places. To do this, a second argument is passed to the round function, which is the number of decimal places.

```python
>>> 8/3
2.6666666666666665
>>> round(8/3,2)
2.67
```

#### 1.3.2 Boolean

Boolean, or relational, expressions are expressions that conceptually result in the values true  or false. The type for these expressions is bool. There are built-in values True and False (note  that these are capitalized). Expressions that result in True are equivalent to the integer 1, and  expressions that result in False are equivalent to the integer 0. The binary relational operators
that can be used in these expressions include:

```python
< less than
> greater than
<= less than or equals
>= greater than or equals
== equality
!= inequality
```

Boolean expressions return the value of True or False.

```python
>>> 3 < 4
True
>>> 6 == 5
False
```

Using the integer remainder division, we can write an expression to test whether an integer is  even or odd. If an integer is even, it will be divisible by 2, so the remainder division operator  would return 0. For example, 8%2 is 0, so 8%2 == 0 would be True. For a variable var, the  expression var%2==0 would be True if the variable is even, or False if it is odd.

```python
>>> var = 16
>>> var % 2 == 0
True
>>> var = 9
>>> var % 2 == 0
False
```

Math can be done on the result of Boolean expressions, since True is the same as 1 and False is  the same as 0.

```python
>>> myval = 3 < 4
>>> myval + 7
8
```

The logical operators operate on Boolean expressions; they are not, and, and or. The not operator is unary; it results in the opposite of the Boolean expression. For example, not True is False, and not False is True. The and and or operators are binary. The or operator returns True
if either or both operands are True. The and operator only returns True if both operands are  True.

```python
>>> 3 < 7 or 2 == 4
True
>>> 3 < 7 and 2 == 4
False
>>> 3 < 7 and 2 == (3 – 1)
True
```

Representing the concepts of true and false is somewhat different. For numbers, 0 represents  the concept of false, but anything that is not 0 can be used to represent the concept of true.  We will see examples and applications of this in later sections and chapters.

#### 1.3.3 Precedence Table

Expressions in parentheses take precedence, or priority, over the operators. There are also  precedence rules for the operators themselves, e.g., multiplication takes precedence over  addition.

For the math and Boolean operators that have been covered so far, the following shows the  operator precedence rules. Operators on each line have priority over the operators below them  in the table.

```python
Parentheses ( )
Exponentiation **
Negation -
Multiplication and Division *, /, //, %
Addition and Subtraction +, -
Relational <, <=, >, >=, ==, != not not
and and
or or
```

When operators have the same precedence, they are evaluated from left to right. This is called  the associativity.

#### 1.3.4 Introduction to Sequences

Numbers and Boolean expressions are simple types that only store one value. Data structures are structured variables that store more than one value. In this section, we will briefly introduce  two types of data structures, strings and lists. Both of these are particular kinds of data  structures called sequences. With sequences, the values are put in an order and can be indexed  using integer indices. Much more information on strings and lists will be covered in Chapters 5  and 7.

##### 1.3.4.1 Strings

Strings in Python are text, and can be stored in either single quotes (‘Hello’) or double quotes  (“Hi!”). A string is a sequence of characters. For example, the following code stores strings in  variables and then prints them.

```python
>>> stringone = 'Hello there'
>>> string2 = "!!!"
>>> print(stringone, string2)
Hello there !!!
```

Printing strings using the print function will not show the quotes. However, displaying the value  of a string variable will. Note that although the variable string2 is created using double quotes,  the default is to display the value of a string with single quotes.

```python
>>> string2
'!!!'
```

The type name for strings is str.

In some languages there is a distinction between a single character and a string of characters,  but in Python they are all strings. A single character is just a string that has only one character in  it.

Strings are composed of individual characters. The individual characters are numbered with  integers beginning with 0. These numbers are called subscripts or indices. For example, for the  variable stringone, the 11 characters have indices from 0 through 10. In the diagram, the  indices are shown above the characters in the string.

```python
0 1 2 3 4 5 6 7 8 9 10
H e l l o t h e r e
```

An individual character can be obtained by putting the index in square brackets after the string  variable name. This is called indexing into the string. For example, the following will print the  first two characters in the string variable stringone.

```python
>>> print(stringone[0], stringone[1])
H e
```

The len function will return the length of the string, which is the number of characters in a  string, e.g.:

```python
>>> len(stringone)
11
```

With a length of 11, the string has indices from 0 through 10.

For strings, indexing returns the individual characters in the string.

The empty string is a string that contains zero characters. An empty string can be created using  quotes with nothing inside, e.g. using single quotes:

```python
>>> len('')
0
```

The in operator will determine whether or not a string is in another string, and return True if it  is or False if it is not. The not in operator will return the opposite.

```python
>>> 'x' in 'abcde'
False
>>> 'x' not in 'abcde'
True
```

Strings are immutable, which means that they cannot be modified. Any attempt to change  character(s) in a string will result in an error message.

```python
>>> myword = 'Hello'
>>> myword[1] = 'a'
TypeError: 'str' object does not support item assignment
```

There are operators for strings. To concatenate, or join strings together, the ‘+’ operator is  used.

```python
>>> 'b' + 'cde'
'bcde'
```

Note that there are no spaces in between the concatenated characters.

Strings can be compared using the relational operators. String comparisons are based on the  character encoding. Two common encoding sequences are ASCII and Unicode. Basically,  characters are put into a sequence and given equivalent integer values. In most encoding  sequences the letters of the alphabet are ordered sequentially, so it is true that ‘a’ is less than  ‘c’ because ‘a’ comes before ‘c’ in the encoding sequence.

```python
>>> 'a' < 'c'
True
```

If one string is shorter than another, but they start with the same characters, the longer string is  greater than the shorter string.

```python
>>> 'ab' < 'abc'
True
```

The print function can print combinations of strings and numbers, e.g.:

```python
>>> string2 = "!!!"
>>> print("The number is", 33, string2)
The number is 33 !!!
```

Note that blanks are automatically inserted in between the text and numbers that are printed.  As we have seen, by default the contents of the strings are printed without quotes around  them.
To print a string variable with quotes around it, the function repr can be used. This function  returns the string representation of the variable (again, always in single quotes).

```python
>>> word = "Monty"
>>> print(word, repr(word))
Monty 'Monty'
```

##### 1.3.4.2 Lists

Lists are sequences of values. Simple lists are created by putting values in square brackets,  separated by commas.

The values in lists can be different types, although it is more common for them to be the same  type.

```python
>>> numlist = [4, 52, 33, 11, -3]
>>> print(numlist, type(numlist))
[4, 52, 33, 11, -3] <class 'list'>
>>> mixedlist = [22, 'hello', 4 > 6]
>>> print(mixedlist, type(mixedlist))
[22, 'hello', False] <class 'list'>
```

Notice that the type of any list is list. Note also that the result of the expression 4>6, False, is  stored in the list.

Since lists are a sequence type, they can be indexed using integers.. However, unlike strings,  lists are a mutable type, which means that they can be modified. The values stored in lists are  called items or sometimes elements. The following creates a list and then indexes into the list  to get the first value (which is in element 0).

```python
>>> numlist = [4, 52, 33, 11, -3]
>>> numlist[0]
4
```

Since lists are mutable, items can be modified by indexing and assigning a new value.

```python
>>> numlist = [4, 52, 33, 11, -3]
>>> numlist[1] = 99
>>> print(numlist)
[4, 99, 33, 11, -3]
```

Lists can contain other sequence types, for example, strings.

```python
>>> strlist = ['hi', 'hello', 'ciao']
>>> strlist[0] = 'howdy'
>>> print(strlist)
['howdy', 'hello', 'ciao']
```

The len function will return the number of elements in a list. There are 3 items in the variable  strlist. The third item in the list (strlist[2]) is a string that has 4 elements, or characters.

```python
>>> len(strlist)
3
>>> len(strlist[2])
4
```

The in operator will determine whether a value is in a list or not.

```python
>>> 4 in numlist
True
>>> 'hello' in strlist
True
>>> 'e' in strlist
False
```

The character 'e' is not one of the elements of strlist, although it is in strlist[1].

#### 1.3.5 Type Casting

Type casting means converting an expression from one type to another. The type names in  Python can be used as function names to accomplish this. For example, to convert x to a float,  use float(x), e.g.

```python
>>> float(4)
4.0
```

Note that in the following, the // operator still returns the result of the integer whole number  division; the integer result of 3 is then converted to the type float:

```python
>>> float(7//2)
3.0
```

Converting a float to an int will truncate the decimal places.

```python
>>> int(5.7)
5
```

A string variable that contains a number can be converted to a number type, e.g.:

```python
>>> strnum = '123'
>>> actualnum = int(strnum)
>>> print(actualnum, type(actualnum))
123 <class 'int'>
```

Conversely, a number can be converted to a string. For example, if we wanted to know how  many digits in a number, we could convert the number to a string and then use the len function  (which does not work on numbers) to get the number of digits:

```python
>>> mynum = 1234
>>> strnum = str(mynum)
>>> print(len(strnum))
4
```

Using the bool function to cast numbers to the type bool, we can see that numbers that are not  0 can be used to represent the concept of true.

```python
>>> print(bool(0), bool(1), bool(33), bool(4.2))
False True True True
```

### 1.4 Modules
We have seen that Python has built-in functions. Many other functions are stored in modules.  Modules in Python can be used to store groups of related functions (and sometimes other  definitions). Modules are separate from the core Python, and must be imported before the  functions contained in them can be used. A module is imported using the import statement,  and then functions contained in the module can be referenced using the dot operator.  Modules are stored in files that have a .py extension on the filename.

There are modules that are built into Python’s standard library, and you can also define your  own modules. Some useful standard modules include the math module, the random module,  and the statistics module. There are also external library modules that have been developed  and are widely distributed. Some of these, such as numpy, pandas, and scipy, contain functions
that are useful in data science applications. The matplotlib module has functions that help to  visualize data. These modules will be introduced in Part II of this book.

The math module contains math functions, as well as some built-in constants. Unlike variables,  constants cannot change. The constants in the math module include:

```python
pi 3.14159
e 2.71828
tau 6.28318
inf infinity
nan not a number
```

Notice that the constant tau is equivalent to 2*pi. The constant e, called Euler’s number, is the  base for natural logarithms. Do not confuse the constant e here with the e used in scientific  notation!

Although by convention user-defined constants are variables that are named using upper case  letters, the constants that are in the math module are named using lower case letters.  Unfortunately, they are not true constants in that their values can be modified.
To use one of them, to calculate π*radius2, for example, we might enter the following:

```python
>>> import math
>>> radius = 3
>>> math.pi*radius**2
28.274333882308138
```

The import statement imports the math module and then the dot operator is used as math.pi  to refer to the constant pi.

The round function could be used here to reduce the displayed number of decimal places.
Note that to use the constant pi, it is necessary to give the name of the module, the dot  operator, and then the name of the constant. In order to make this simpler, and avoid the use  of the dot operator, certain or all constants and functions from a module can be imported using  the from statement. For example, to just import pi:

```python
>>> from math import pi
```

After importing pi, just the name pi can be used without first specifying math and the dot  operator.

```python
>>> from math import pi
>>> radius = 3
>>> round(pi*radius**2,2)
28.27
```

To import both pi and e:

```python
>>> from math import pi, e
```
To import everything:
```python
>>> from math import *
```

The * is sometimes called a wildcard and in this case means everything. Importing everything  from a module is not generally recommended since you probably do not know the names of  everything that will be imported, and some names could interfere with names that you already  have (variable names, for example).

Once the math module has been imported, all of the constants and functions can be seen using  the help function.

```python
>>> help(math)
```

The math module contains many useful math functions. These include trig functions such as  sin, cos, and tan. Another function that is used a lot is the square root function, sqrt. There is  also a function exp, which returns the constant e raised to a specified power.

To read about a particular function, use the dot operator. For example,

```python
>>> help(math.sqrt)
Help on built-in function sqrt in module math:
sqrt(x, /)
Return the square root of x.
```

### 1.5 Objects and Methods

Python is based on objects. Objects have special functions, called methods, that are associated  with every type. Methods are different from functions in that, instead of explicitly passing an  expression to them in parentheses, they are called implicitly with an expression using the dot  operator.

For example, for strings there is a method called upper, which will convert all letters of the  alphabet in a string to upper case.

```python
>>> mychars = 'Hello123'
>>> mychars.upper()
'HELLO123'
```

This displays the letters in the string in upper case, but it does not change the variable mychars.  (Recall that string variables are immutable; they cannot be changed.) The string variable  mychars is not passed explicitly to the upper method, but rather is passed implicitly by using  the dot operator. In this case, there is no need to pass any arguments so the parentheses after  the method name are empty. It is necessary, however, to have the empty parentheses. Note  that any non-alphabetical characters are not changed.

If it is desired to change the variable, the result of the expression must be assigned back to the  variable.

```python
>>> mychars = 'Hello123'
>>> mychars = mychars.upper()
>>> mychars
'HELLO123'
```

Similarly, there is a method called lower that will convert letters in a string to lower case.
In the previous example, a variable was used as the calling expression, but that is not necessary.  The calling expression in this case can be just a string.

```python
>>> 'Hello123'.lower()
'hello123'
```

Another method for strings is index, which returns the index of the first occurrence of a  specified character, or the beginning of a specified substring. Recall that the indices begin at 0.

```python
>>> urname = 'monty python'
>>> urname.index('y')
4
>>> urname.index('py')
6
```

Note that with the index method, the string is passed implicitly using the dot operator, and the  substring is passed explicitly in parentheses. The call to the method urname.index(‘y’) is asking  for the location of the string ‘y’ in the variable urname.

Sometimes it is not known whether the letters in a string are lower or upper case, so they can  be converted to all lower (or upper) before finding an index.

```python
>>> urname = 'Monty Python'
>>> urname.lower().index('py')
6
```

Notice the use of the dot operator twice here. First, the lower method was used to convert the  string to lower case, and then the index method was used to find the location of ‘py’.

There are some methods that return True or False. For example, there are “is” methods that  ask a question and return either True or False. The islower method will test to see whether or  not all letters of the alphabet in a string are lower case.

```python
>>> mychars = 'Hello123'
>>> mychars.islower()
False
>>> mychars = 'hello123'
>>> mychars.islower()
True
```

Similarly, the isupper method will test to see whether or not all letters of the alphabet in a  string are upper case.

Another method that can be used with strings is startswith, which determines whether or not a  string starts with a particular character or string, and returns True if it does or False if it does  not.

```python
>>> word = "Monty"
>>> print(word.startswith('Mo'), word.startswith('&')) True False
```

In this case the startswith method is called with the string variable word, and a string is passed  as an argument to test to see whether or not the variable begins with that string (of one or  more characters). Similarly, there is a method endswith.

More string methods will be covered in Chapter 7.

There are methods for all variable types in Python, not just strings. For float numbers, for  example, the method is_integer will return True if the value stored is actually an integer or  False if it is not.

```python
>>> num = 33.0
>>> print(type(num))
<class 'float'>
>>> num.is_integer()
True
```

There are many methods that can be used with lists. The index method can be used with lists as  well as strings. For example,

```python
>>> [4, 33, 11, 5].index(11)
2
```

### 1.6 Random Numbers

It is often useful to be able to generate random numbers. The random module has several  functions that facilitate this.

The randint function will return a random integer. Called as randint(a,b), it will return a random  integer in the inclusive range from a to b. For example, the following prints a random integer in  the inclusive range from 2 to 10.

```python
>>> from random import randint
>>> print(randint(2,10))
5
```

The random function returns a random real number in the range from 0 to 1, not including 1.  No arguments are passed to it, so when calling it the parentheses are empty.

```python
>>> from random import random
>>> rf = random()
>>> rf
0.6405322431584719
```

Another function in the random module is the choice function, which chooses and returns a  random item from a sequence. For example, the choice function can choose a random  character from a string.

```python
>>> from random import choice
>>> mystring = 'abc*&def'
>>> choice(mystring)
'c'
```

We will see examples using other sequence types in later chapters.

### 1.7 Help Utility

We have seen that the help function can be used to show the functions in a given module. For  example, help(math) will display information about the math module once the math module  has been imported. To find out about a particular function in a module, use the dot operator,  e.g., help(math.sqrt).

The help function can also be used to display information about a particular function that is in  core Python, e.g., help(round) will explain the usages of the round function.
To find out what methods can be used with expressions and variables of a particular type, pass  the name of the type to the help function. For example, help(str) will display a list of the  methods that can be used with strings. To find out about a particular method, use the dot  operator. For example,

```python
>>> help(str.islower)
Help on method_descriptor:
islower(self, /)
Return True if the string is a lowercase string, False otherwise.
A string is lowercase if all cased characters in the string  are lowercase and there is at least one cased character in  the string.
```

A slightly more readable version can sometimes be obtained using a variable that has been  created:

```python
>>> word = "Monty"
>>> help(word.islower)
Help on built-in function islower:
islower() method of builtins.str instance
Return True if the string is a lowercase string, False otherwise.
A string is lowercase if all cased characters in the string  are lowercase and there is at least one cased character in  the string.
```

Typing just help(), without any arguments, brings up a help utility, which has a special prompt  of help>. At this prompt, the following can be entered:

```python
modules shows a list of all available modules
keywords shows a list of all keywords
symbols shows a list of all symbols that are used as operators
topics shows a list of all documentation topics
quit exits the help utility
```

Keywords (also called reserved words) are words that are built in to Python and can never be  used as variable names. These include commands such as import.
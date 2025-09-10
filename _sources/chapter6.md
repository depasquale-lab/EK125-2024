Chapter 6 More on Programming

6.1 User-Defined Functions

We have seen many built-in functions in Python. You can also write your own functions, which are called user-defined functions.  Related user-defined functions can be stored in user-defined modules, which can then be imported into programs for use.

When we write a function, we write the function definition. The function can then be called, much like built-in functions.

The general form of a function definition is:

def functionname(parameters):
""" Documentation string. """
# Function body

The first line is called the function header. It consists of the reserved word def, the name of the function, parameters (if any) in parentheses, followed by a colon. The rest of the function, which is indented, is the function body. This typically begins with a documentation string (docstring), in triple quotes. The docstring should be sentence(s) describing what the function does, beginning with a capitalized word and ending with a period.  After the docstring there are the statements in the body of the function.  It is common to indent the body of the function 4 spaces.

The function is called by giving the name of the function, and passing arguments in parentheses that will correspond to the parameters in the function header:

functionname(arguments)

Sometimes the arguments in the function call are referred to as actual parameters and the parameters in the function header are referred to as formal parameters.

Although this is somewhat arbitrary, we will begin with two types of functions:
Functions that calculate and return a value
Functions that accomplish a task

Two main reasons for writing our own functions are:
To be able to reuse code by calling the function whenever it is needed
To write modular programs

If there is code that will be repeated at different times, perhaps using different values, it can be made into a function and then called whenever needed.

Modular programs are programs that consist of a series of functions that do the actual work. The functions are called by a main program, which can be implemented as either a script or function.

6.1.1 Functions with Return

We have seen examples of built-in functions that calculate and return a value, such as the round function.  User-defined functions can also accomplish this using the return statement.

As an example, we will write a function that returns the area of a square. In order to calculate the area of a square, the function needs the length of each side of the square, so the side length must be passed as an argument to the function. Here is a function definition for a function named sqrarea that accomplishes this:

def sqrarea(sidelen):
"""This function calculates the area of a square."""
sqar = sidelen**2
return sqar

The function can then be called by using the name of the function and passing a number for the length of a side of the square:

>>> sqrarea(3)
9

In the function call, the side length, 3, was passed to the parameter sidelen in the function. The function then squared this, and returned the result.  We say that when the function is called, control is sent to the function, and the function begins executing. The return statement not only returns the value (in this case, 9), but also sends control out of the function.

In general a docstring describes what a function does and can be displayed using the help function:

>>> help(sqrarea)
Help on function sqrarea in module __main__:

sqrarea(sidelen)
This function calculates the area of a square.

The variable sqar, which was used in the function body, was not necessary. The return statement could just return an expression:

def sqrarea(sidelen):
"""This function calculates the area of a square."""
return sidelen**2

The value returned from the function would normally be stored in a variable, e.g.

>>> mysquare = sqrarea(3)
>>> mysquare
9

In this example, one argument was passed to the function.  For a function to calculate the area of a rectangle, both the length and width of the rectangle must be passed to the function, so there will be two parameters in the function header and two arguments passed in the function call:

def rectarea(rlen, rwid):
"""This function calculates the area of a rectangle."""
return rlen * rwid

>>> rectarea(2, 4)
8

The values of the arguments are passed to the corresponding parameters in the function, so the first argument, 2, is passed to the first parameter rlen, and the second argument 4 is passed to the second parameter rwid.

Notice that the return statement returned the result of an expression; an intermediate variable could be used but is not necessary.

In Python, the return statement can only return one object. If it is desired to have a function return more than one thing, they can be stored in one data structure (such as a tuple or list), and that can be returned.  In the following example, a function calculates and returns both the area and the perimeter of a square, by storing both in a list.

def sqrarea_perim(sidelen):
"""Calculates the area and perimeter of a square."""
sqar = sidelen**2
sqperim = 4 * sidelen
results = [sqar, sqperim]
return results

>>> sqrarea_perim(11)
[121, 44]

Using a tuple instead of a list is perhaps easier to understand, and it is easier to use the results.

def sqrarea_perim(sidelen):
"""Calculates the area and perimeter of a square."""
sqar = sidelen**2
sqperim = 4 * sidelen
return sqar, sqperim

>>> area, perim = sqrarea_perim(11)
>>> print(area, perim)
121 44

6.1.2 Functions with no Return

In many cases functions calculate and return values, but in some cases functions just accomplish a task, such as printing.

For example, the following function receives as parameters a string and an integer n, and prints the string n times in a row on one line. After that, it moves the cursor down.

def printstrs(instr, n):
"""This function prints instr n times."""
for i in range(n):
print(instr,end='')
print()

Here are two examples of calling the function:

>>> printstrs('x',3)
xxx

>>> printstrs("Hi", 5)
HiHiHiHiHi

Notice that the function does not have a return statement, since it is not calculating anything.  However, all functions return something regardless of whether there is a return statement or not. The default value that is returned is a special value None, as we can see by passing a call to the function printstrs to the print function.  In the following example, ‘aa’ and then the newline gets printed by the function, and then the result returned by the function call, None, is printed once the function stops executing and returns control.

>>> print(printstrs('a',2))
aa
None

The printstrs function prints the line ‘aa’ and returns None. The print function then prints the returned value, None.  This is equivalent to:

>>> x = printstrs('a',2)
>>> print(x)

It is not always necessary to pass arguments to functions (whether they explicitly return something or not).  For example, we may wish to have a function that just prints a set of instructions.

def printinstruct():
"""This function just prints stuff."""
print('Please sit up')
print('Do not slouch!')
print('Chew with your mouth closed')

>>> printinstruct()
Please sit up
Do not slouch!
Chew with your mouth closed

A function like this that just prints helps to facilitate modular programs. Of course, the instructions printed by a function would normally refer to actions that the user must take when running a program!

6.1.3 Scope

The scope of a variable or object is where that object is valid. For functions, everything that is defined in the function is valid only in that function. We say that variables defined in a function are local to that function, meaning that their scope is the function. Formally, what happens is that every function has its own symbol table, which contains the names of the variables and their values. Once a function is called and control is sent to the function, its symbol table is created. The function’s symbol table only exists while the function is executing.

For example, for the sqarea function, the symbol table contains the local variable sqar, as well as the parameter sidelen.

def sqrarea(sidelen):
"""This function calculates the area of a square."""
sqar = sidelen**2
return sqar

After the function is called, attempting to reference either sqar or sidelen will result in an error.  This is because after the function stops executing, the symbol table, the variable sqar, and the parameter sidelen no longer exist.

>>> area = sqrarea(4)
>>> print(sqar)

NameError: name 'sqar' is not defined

6.1.4 Lambda Functions

Anonymous functions, called lambda functions in Python, are very short one line functions that do not require a formal function definition using def.  Lambda functions are created using the keyword lambda. The general form is:

lambda argument(s): expression

The function begins with the reserved word lambda, then argument(s) followed by a colon and then an expression that uses the arguments; the result of the expression is returned.

If the lambda function is stored in a variable, the variable can be used to call the function. For example,
>>> times3 = lambda num: num * 3
>>> times3(11)
33

One advantage of a lambda function is that it is shorter than a function definition and does not require the header with def or the return statement. A disadvantage is that the “body” of the function is confined to one simple expression.

6.2 Assignment Statements and Copying

Assignment statements basically assign a value to a variable. Another way of saying this is that the assignment binds the variable to the value.

We have seen that variables refer to locations in which values are stored.  What happens when one variable is assigned to another variable, e.g.

var2 = var1

is that they both refer to the same location. This has interesting ramifications when modifying variables, especially for mutable types.

Assigning an expression (not another variable) to a variable in assignment statements creates a new location for the variable to reference, and stores the result of the expression in that location. Assigning another variable, however, does not create a new location; instead, both variables now refer to the same location.

Consider the following code:

>>> x = 4
>>> y = x

What happens is that the variable x is created, and it refers to a location in which a 4 is stored. Then, assigning x to y means that y is now also going to refer to the same location as x. We can picture this as follows:


Then, assume that the following assignment statement is executed:

>>> x = 5

This creates a new location in which a 5 is stored, and x now refers to that new location. The variable y, however, has not been changed. It still refers to the location in which 4 is stored.

>>> x
5
>>> y
4

This may seem like a nuance, but it is very important especially for mutable types.

In the next section, operators and functions that illustrate how this works will be introduced.

6.2.1 Variable Identities

Before we examine assigning one variable to another, let us first revisit assignment statements and how they work. One important piece of information is that every location that a variable references is assigned a unique identity. The value of this identity can be found with the id function.  In some cases the identity is the actual address of the location that the variable refers to. Regardless of whether this is true or not, every variable has a unique identity number. Do not try to make sense of the actual numbers!

>>> varname = 11
>>> print(id(varname))
140662851902064

What actually happens when we assign a value to a variable, and then reassign a different value to that variable? We can print the value of the variable and its identity to see what happens.

>>> var1 = 5.3
>>> print(var1, id(var1))
5.3 140663007004368

>>> var1 = 11.11
>>> print(var1, id(var1))
11.11 140663007003760

We can see that the value changed, but the identity did, also. This means that the second assignment did not actually modify what was stored in the original location referred to by var1, but rather created a new location.

This happens also if we modify the value of the variable by multiplying the current value by 2.

>>> var1 = 5.3
>>> print(var1, id(var1))
5.3 140663007003280

>>> var1 = var1 * 2
>>> print(var1, id(var1))
10.6 140663007003888

Again, the second assignment created a new location and stored the result of the expression on the right (var1 * 2) in that location, and var1 now refers to the new location.

Let’s now see what happens when we assign one number variable to another.  We can see the locations using the id function. However, when comparing two identities, it is simpler to use the is operator. The is operator can be used to determine whether two variables refer to the same location, or in other words, whether their identities are the same or not.  The expression a is b results in True if a and b refer to the same location (have the same identities) or False if not.

radius = 3
rad = radius
print(radius, id(radius))
print(rad, id(rad))
if rad is radius:
print('They are the same')
else:
print('They are not the same')
print()
radius = 5
print(radius, id(radius))
print(rad, id(rad))
if rad is radius:
print('They are the same')
else:
print('They are not the same')
3 140437299009904
3 140437299009904
They are the same

5 140437299009968
3 140437299009904
They are not the same

We can see that after the initial assignment rad = radius the two variable names referred to the same location. However, the assignment radius = 5 then created a new location, a new identifier, for the variable radius to refer to.

There is also an is not operator.  The expression
a is not b
is equivalent to
not (a is b)
but is easier to read and understand.

The same behavior can be seen for other simple types like Boolean, and for immutable types such as strings and tuples, as shown in the following simplified examples:

>>> relate = 6 < 10
>>> isit = relate
>>> print(relate, isit)
>>> isit = 6 > 10
>>> print(relate, isit)
True True
True False

>>> word = "hello"
>>> greetword = word
>>> print(word, greetword)
>>> word = "hi"
>>> print(word, greetword)
hello hello
hi hello

>>> tupone = (5, 11, 'x')
>>> tuptwo = tupone
>>> print(tupone, tuptwo)
>>> tupone = (4.4, 39)
>>> print(tupone, tuptwo)
(5, 11, 'x') (5, 11, 'x')
(4.4, 39) (5, 11, 'x')

For lists, assigning  a new list to one of the list variables results in the same behavior that has been seen with other types.

listone = [5, 11, 'x']
listtwo = listone
print(listone, listtwo)
if listtwo is listone:
print('They are the same')
else:
print('They are not the same')
print()
listone = ['q', '?', 0]
print(listone, listtwo)
if listtwo is listone:
print('They are the same')
else:
print('They are not the same')
[5, 11, 'x'] [5, 11, 'x']
They are the same

['q', '?', 0] [5, 11, 'x']
They are not the same

This is because again, all assignments create a new location for the variable to refer to.  However, lists are different in that they are mutable. This means that the contents of a list can be modified. Changing the contents of a list variable is different from assigning a brand new list!

listone = [5, 11, 'x']
listtwo = listone
print(listone, listtwo)
if listtwo is listone:
print('They are the same')
else:
print('They are not the same')
print()
listone[1] = 27
print(listone, listtwo)
if listtwo is listone:
print('They are the same')
else:
print('They are not the same')
[5, 11, 'x'] [5, 11, 'x']
They are the same

[5, 27, 'x'] [5, 27, 'x']
They are the same

This means that the two list variables refer to the same location, and the contents of one of the items in the list was modified – but no new lists were created, so the variables still referred to the same location at the end of the code.  This same behavior will occur any time a list is modified.

We have seen that in Python, for the types that we have covered so far, assigning one variable to another creates an alternate reference to the same location.

Beware of list slices, however! Slicing a list using just the colon is different from using the variable name.

>>> listone = [5, 11, 'x']
>>> listtwo = listone
>>> listthree = listone[:]
>>> print(listone, listtwo, listthree)
>>> print(id(listone), id(listtwo), id(listthree))
[5, 11, 'x'] [5, 11, 'x'] [5, 11, 'x']
140663007067328 140663007067328 140663007088192

We can see here that the variables listone and listtwo refer to the same location, but by using the slice operator and assigning the result to listthree, the listthree variable refers to a separate location.  This does not happen with strings or tuples, however, because they are immutable.

>>> strone = "hi"
>>> strtwo = strone
>>> strthree = strone[:]
>>> print(strone, strtwo, strthree)
>>> print(id(strone), id(strtwo), id(strthree))
hi hi hi
140662877875888 140662877875888 140662877875888

6.2.2 Shortcut Assignments

Python has what are called shortcut assignment operators.  These add no power to the language, but save a little typing.

For example, the statement num += 1 is equivalent to the statement num = num + 1.

>>> num = 4
>>> num += 1
>>> num
5

This also works for concatenation, e.g.:

>>> str = 'hi'
>>> str += 'x'
>>> str
'hix'

The shortcut is that instead of typing the name of the variable twice, once on the left and once on the right of the assignment operator =, we put the + to the left of the assignment operator and then only have to type the name of the variable once.

This also works for other operators, e.g. using *= to multiply:

>>> inumb = 3
>>> inumb *= 2
>>> inumb
6

This takes the current value of the variable inumb, multiplies by 2, and stores the result in a new location pointed to by the variable inumb.

Note that for mutable types, shortcut assignments modify the contents of the variable rather than creating a new variable.

>>> list = [1, 5, 33]
>>> print(list, id(list))
[1, 5, 33] 140437475761920

>>> list += [14]
>>> print(list, id(list))
[1, 5, 33, 14] 140437475761920

>>> list = list + [29]
>>> print(list, id(list))
[1, 5, 33, 14, 29] 140437475751424

6.2.3 Simultaneous Assignments

We have seen the simultaneous assignment statement, in which there are multiple variables on the left of the assignment operator, and an equal number of expressions on the right. For example, the following code initializes the variables mysum and mycount to have the value 0.

>>> mysum, myproduct = 0, 1

Simultaneous assignments can be used to exchange the values of two variables. The following code does not produce the desired result, since the assignment a = b will assign 10 to the variable a, and the original value of a (which was 3) is lost.

>>> a = 3
>>> b = 10
>>> print(a,b)
>>> a = b
>>> b = a
>>> print(a,b)
3 10
10 10

Generally in programming it is necessary to use a temporary variable for this.

>>> a = 3
>>> b = 10
>>> print(a, b)
>>> temp = a
>>> a = b
>>> b = temp
>>> print(a,b)
3 10
10 3

By storing the original value of a in the variable temp, the value is not lost and can then be assigned to b.

However, in Python this can be accomplished using the simultaneous assignment, since the assignments can be thought of as simultaneous and not sequential.

>>> a, b = 3, 10
>>> print(a,b)
>>> a,b = b,a
>>> print(a,b)
3 10
10 3

6.2.4 Passing Arguments to Functions

In Python, arguments are passed to functions using a methodology that is sometimes referred to as call-by-assignment.  That is, passing arguments to function parameters in Python works in the same way as assigning one variable to another variable. Passing an argument to a function parameter results in the function parameter referring to the same location as the argument.

The following example illustrates this for an argument which is an immutable type, in this case a number.

def testcall(mynum):
""" Tests results of a function call with a number argument. """
print('Fn: ', mynum, id(mynum))
mynum = 14
print('Fn: ', mynum, id(mynum))


>>> num = 5
>>> print(num, id(num))
>>> print('Now function is called')
>>> testcall(num)
>>> print('Function has ended')
>>> print(num, id(num))
5 140503077231024
Now function is called
Fn:  5 140503077231024
Fn:  14 140503077231312
Function has ended
5 140503077231024

In this example, the integer 5 was assigned to a variable num, and the value that num refers to and its id were printed. Then, the function was called. This causes the parameter mynum in the function to refer to the same location that num refers to. This can be seen from the result of the first print statement in the function. Then, a new value, 14, was assigned to mynum which means that mynum now refers to a new location in which the 14 is stored. The function ends at that point, and we can see that after the function has finished executing, the variable num has not changed.

Similar results will be obtained for other immutable parameter types, such as strings or tuples.

Now let’s try basically the same example, but using a list instead of a number. Since assignment statements always create a new location, the result is similar to the result when the argument is a number.

def testcalllist(mylist):
""" Tests results of a fn call with a list argument. """
print('Fn: ', mylist, id(mylist))
mylist = [33, 5, 11]
print('Fn: ', mylist, id(mylist))

>>> listarg = [44, 2, -99]
>>> print(listarg, id(listarg))
>>> print('Now function is called')
>>> testcalllist(listarg)
>>> print('Function has ended')
>>> print(listarg, id(listarg))

[44, 2, -99] 140503223213248
Now function is called
Fn:  [44, 2, -99] 140503223213248
Fn:  [33, 5, 11] 140503223315136
Function has ended
[44, 2, -99] 140503223213248

However, if the list parameter is modified within the function (instead of assigning a new list), the list argument that was passed to the function will change.

def testcalllistchg(mylist):
""" Tests results of a fn call with a list argument. """
print('Fn: ', mylist, id(mylist))
mylist.append(8)
print('Fn: ', mylist, id(mylist))

>>> listarg = [44, 2, -99]
>>> print(listarg, id(listarg))
>>> print('Now function is called')
>>> testcalllistchg(listarg)
>>> print('Function has ended')
>>> print(listarg, id(listarg))

[44, 2, -99] 140503223251712
Now function is called
Fn:  [44, 2, -99] 140503223251712
Fn:  [44, 2, -99, 8] 140503223251712
Function has ended
[44, 2, -99, 8] 140503223251712

In many cases, having the function modify the list variable is not a desired outcome. To protect the list from being changed, a slice consisting of the entire list can be passed instead of just the list variable:

>>> listarg = [44, 2, -99]
>>> print(listarg, id(listarg))
>>> print('Now function is called')
>>> testcalllistchg(listarg[:])
>>> print('Function has ended')
>>> print(listarg, id(listarg))

[44, 2, -99] 140503223187200
Now function is called
Fn:  [44, 2, -99] 140503223252480
Fn:  [44, 2, -99, 8] 140503223252480
Function has ended
[44, 2, -99] 140503223187200

6.3 Modular Programs

In general in programming, a modular program is one in which the program is broken down into separate tasks, and each task is implemented as a function. This facilitates the top-down design approach of taking a problem, breaking it down into pieces, and implementing each as a function.  The program then consists basically of calling the functions to complete each of the tasks.

A basic algorithm for many programs is:
Get input(s)
Calculate result(s), using the input(s)
Print and/or display the result(s)

So, a simple outline of many programs would be to have:
Function(s) to get the input(s)
Function(s) to calculate result(s) using the input(s)
Function(s) to display the result(s)

As an example, we will write a program that will prompt the user for the cost of an item in a store, and then calculate and print the total cost with a tax of 3%.  The program will call 3 functions:
A function to prompt for and return the cost
A function to calculate the total cost including the tax
A function to print the total cost

Here are the function definitions.

def getcost():
""" Prompts for item cost. """
cost = float(input('Enter the item cost: '))
return cost

def calctax(cost):
""" Calculates and returns cost plus tax. """
tax = cost * .03
return cost + tax

def printtotcost(totcost):
""" Prints cost plus tax. """
print(f'The total cost is ${totcost:.2f}')

The functions could be called from a script, which is frequently called a main program. The program consists of calls to the functions.

# main program
cost = getcost()
totalcost = calctax(cost)
printtotcost(totalcost)

The output might look like this:

Enter the item cost: 11.11
The total cost is $11.44

Of course, to be more complete, the getcost function would error-check to make sure that the user enters a valid cost.

Sometimes the main program is implemented as a function rather than a script.

6.3.1 Function Stubs

When writing a program that consists of a script calling multiple functions, the best practice is not to write the entire program and then execute it to see the results. Frequently, there are errors. When an error is encountered in a particular function, the problem may be in that function, or it might be the result of an incorrect argument passed to the function, that was obtained from another function. A more effective method for constructing the program is to use function stubs, which are place-holders for the actual functions.

The approach is:
Sketch out the algorithm
Decide what the functions are going to do
Write the script, consisting of the calls to the functions (including the arguments that will get passed back and forth)
Write function stubs for the individual functions
Change each function stub to the actual function, one at a time

This methodical method of writing a program helps cut down on mistakes, and makes it easier to find bugs when they occur.

Function stubs should mimic what the function is eventually going to do, including using the arguments and returning the correct type(s).

For example, let’s say we are going to write a program that will prompt the user for a temperature in degrees Celsius, convert that to Fahrenheit, and print the results.

We might have functions to:
Prompt the user for degrees C, error-checking to make sure it’s valid, and return the result
Receive the degrees C and from that calculate and return degrees F
Print both degrees C and degrees F in a nice sentence format

The script for the main program might look like this:


# Convert C to F
degC = getdegc()
degF = c2f(degC)
printCF(degC, degF)

Example function stubs might look like this:

def getdegc():
“””Prompts user for degrees Celsius.”””
return 33

def c2f(degreesc):
“””Converts degrees C to degrees F”””
return degreesc + 5


def printCF(degreesc, degreesf):
“””Prints degrees C and degrees F”””
print(degreesc, degreesf)

The idea is to execute the program with the function stubs and make sure that values are being passed back and forth correctly. Eventually, after prompting the user and error-checking, the getdegc function will return a positive number. So, for now, we just return a positive number. Eventually, once we figure out the conversion, the c2f function will convert C to F. For now, we’ll just add 5 so we know that this function is correctly receiving the degrees C and using this number to calculate and return degrees F. Then, the printCF function will eventually print in a nice sentence format, but for now it will just print the values.

The headers for the functions should not change. Putting the actual doc strings in the function stubs is a good idea.

Then, once that is working, modify the stubs one at a time. For example, you might start by modifying the getdegc function to prompt the user. Then, modify that function to include the error-checking.  Going about this systematically really does cut down on errors and makes it easier to find them.
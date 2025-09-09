Chapter 5 Data Structures

This chapter will cover data structures.  Data structures, or structured variables, are used to store more than one value. These are also called compound types. We have already seen two types of data structures, string, which store multiple characters, and lists. Recall that strings and lists are examples of a particular type of data structure called a sequence. With sequences, the values are put in an order and can be indexed using integer indices. Another simple type of sequence data structure, which is used very commonly in Python, is a tuple.  We will also cover more detail on the range function, as well as enumerate.

5.1 Strings

We have seen that strings in Python are text, and can be stored in either single quotes or double quotes. Strings are an example of a particular kind of data type called a sequence.  Sequences in general are collections of values (for strings, collections of characters) that can be indexed using integers.  For strings, indexing returns the characters in the string.

We have seen indexing into a string starting at the beginning uses positive integer indices, beginning with 0. Negative indices can be used to index into a string from the end of a string. Using an index of -1 returns the last character in a string, regardless of how long it is.

>>> myword = 'hello'
>>> myword[-1]
'o'

For this string, with a length of 5, an index of -5 will return the first character.

>>> myword = 'hello'
>>> myword[-5]
'h'

So, note that with a string that has a length of 5, the positive indices go from 0 through 4, and the negative indices go from -1 through -5 (in reverse order).

Strings can also be sliced.  A slice of a string is a subset of the characters in the string. This is also sometimes called a substring. The colon operator is used in a variety of formats to create string slices.  The colon operator specifies the beginning index (which is included in the string that is returned), and the ending index (which is not included).

The following example returns the characters in indices 0 and 1:

>>> myword = 'hello'
>>> myword[0:2]
'he'

The following example only returns the character in index 2 (which is the second from the end):

>>> myword = 'help'
>>> myword[-2:-1]
'l'

The starting and/or ending indices can also be omitted. If the starting index is not specified, the default is 0 (the first index), and if the ending index is not specified, the default is the length of the string.

The following example is equivalent to myword[3:5] so it returns the characters in indices 3 and 4:

>>> myword = 'hello'
>>> myword[3:]
'lo'

The following example is equivalent to myword[0:1] so it returns the character in index 0:

>>> myword = 'hello'
>>> myword[:1]
'h'

This means that just using a colon, without specifying any indices, returns a slice consisting of the entire string.

>>> myword = 'hello'
>>> myword[:]
'hello'

When indexing into a string, a second colon can be used, and the third value indicates a step. For example, the following specifies a slice of a string beginning at index 3, through index 9 (since 10 is specified), in steps of 2, which means every other character, beginning with the fourth.

>>> mystr = 'helloabcde'
>>> print(mystr[3:10:2])
lace

Using a negative step means indexing into the  string in reverse order, so the first index specified should be larger than the second.

>>> mystr = 'helloabcde'
>>> print(mystr[7:2:-2])
cal

Just specifying the step of 2 will return every other character, from the beginning:

>>> mystr = 'helloabcde'
>>> mystr[::2]
'hlobd'

Only specifying a step of -1 will reverse a string.

>>> mystr = 'helloabcde'
>>> mystr[::-1]
'edcbaolleh'

We have seen the concatenation operator +, which concatenates strings together. Notice that concatenating slices obtained by using the same number, first for the ending index (omitting the starting index), and then for the starting index (omitting the ending index), results in the entire string. The following concatenates ‘hel’ with ‘lo’:

>>> myword = 'hello'
>>> myword[:3] + myword[3:]
'hello'

To concatenate a string with itself n times, where n is an integer, the ‘*’ operator is used.

>>> news = 'cde'
>>> news*3
'cdecdecde'

Two functions, ord and chr, can be used to convert a character to its integer equivalent, and to convert an integer to its character equivalent, respectively. The function ord returns the Unicode code for a character, and chr returns a string consisting of one character:

>>> ord('a')
97

>>> chr(97)
'a'

>>> ord('b')
98






Although the letters of the alphabet are in sequence, there are other characters in the Unicode encoding sequence before the letters start. Also, the upper case letters are together in the encoding sequence, and the lower case letters are together, but there are other characters in between the upper and lower case letters.

>>> ord('A')
65

>>> ord('B')
66

>>> ord('a') - ord('Z')
7

We have seen that the str type has methods, including index.

Using index, and slicing, we can break a string into pieces. The following indexes into the name to find the location of the space between the first and last names, and then slices up to that location to get just the first name.

>>> urname = 'monty python'
>>> wherespace = urname.index(' ')
>>> firstname = urname[:wherespace]
>>> firstname
'monty'

Since the input function returns a string, text processing must be used to split the string into multiple values if multiple inputs are desired.  For example, the following prompts the user for the length and width of a rectangle. It finds the location of the space in between them, and separates the string into the two values. It then converts both to numbers and calculates and prints the area of the rectangle.

print('When prompted, enter the length and width of a rectangle')
lenwid = input('Separate with a space: ')
wherespace = lenwid.index(' ')
len = float(lenwid[:wherespace])
wid = float(lenwid[wherespace+1:])
print("Area = ", round(len * wid, 2))

When prompted, enter the length and width of a rectangle
Separate with a space: 3.1 4.4
Area =  13.64




5.2 Lists

Lists are sequences of values. Simple lists are created by putting values in square brackets, separated by commas. As we have seen, the values in lists can be different types, although it is more common for them to be the same type.

The len  function returns the number of elements in a list..

>>> numlist = [4, 52, 33, 11, -3]
>>> len(numlist)
5

An empty list can be created using square brackets with nothing inside.

>>> el = []
>>> len(el)
0

Since lists are a sequence type, they can be indexed using integers and they can be sliced.

>>> numlist = [4, 52, 33, 11, -3]
>>> numlist[0]
4

>>> numlist = [4, 52, 33, 11, -3]
>>> numlist[-2:]
[11, -3]

The del statement can delete item(s) from a list.  This will actually modify the list variable.

>>> numlist = [4, 52, 33, 11, -3]
>>> del numlist[1]
>>> numlist
[4, 33, 11, -3]

>>> numlist = [4, 52, 33, 11, -3]
>>> del numlist[1:3]
>>> numlist
[4, 11, -3]

Assigning the empty list to item(s) is another way to delete items (besides using del).

>>> numlist = [4, 52, 33, 11, -3]
>>> numlist[0:2] = []
>>> numlist
[33, 11, -3]

Since lists are mutable, items can be modified by either indexing or slicing and assigning new value(s).

>>> numlist = [4, 52, 33, 11, -3]
>>> numlist[1] = 99
>>> print(numlist)
[4, 99, 33, 11, -3]

>>> strlist = ['hi', 'hello', 'ciao']
>>> strlist[0] = 'howdy'
>>> print(strlist)
['howdy', 'hello', 'ciao']

>>> numlist = [4, 52, 33, 11, -3]
>>> numlist[3:] = [7, 8, 9]
>>> print(numlist)
[4, 52, 33, 7, 8, 9]

Notice that the number of items being replaced does not have to be the same as the number of items replacing them.

An entire list can be obtained using the slice operator, as in:

>>> numlist = [4, 52, 33, 11, -3]
>>> numlist[:]
[4, 52, 33, 11, -3]

However, caution should be used with this because in some contexts, this is different from just referring to the list variable. We will see more on this in Section 6.1.

Lists of characters can be created from strings using the list function.

>>> list("monty")
['m', 'o', 'n', 't', 'y']

The choice function, which is in the random module, can be used to choose a random item from a list.

>>> from random import choice
>>> numlist = [4, 52, 33, 11, -3]
>>> choice(numlist)
33



The shuffle function randomly organizes the items in a sequence.  For example, the shuffle function is used to modify the order of a list in the following.

>>> numlist = [4, 52, 33, 11, -3]
>>> from random import shuffle
>>> shuffle(numlist)
>>> numlist
[33, -3, 52, 11, 4]

Operators and functions can be used on lists.  For example, lists can be concatenated using the + operator.

>>> numlist = [4, 52, 33, 11, -3]
>>> newnums = numlist + [25]
>>> print(newnums)
[4, 52, 33, 11, -3, 25]

The concatenation operator can only concatenate one list to another (not an individual value to a list), which is why the 25 is in square brackets.

The in operator will determine whether or not a value is in a list, and return True if it is or False if it is not.

>>> numlist = [4, 52, 33, 11, -3]
>>> 33 in numlist
True

Statistical functions can be called to perform operations on lists such as min for the minimum value in a list and max for the maximum value.

>>> min(numlist)
-3

>>> max(numlist)
52

There is also a built-in function sum that will sum the numbers in a list of numbers:

>>> numbers = [5, 11, 4]
>>> sum(numbers)
20




An error will occur if the list contains values, for example strings, that cannot be added using sum.

>>> slist = ['hi', 'hello', 'ciao']
>>> sum(slist)

TypeError: unsupported operand type(s) for +: 'int' and 'str'

Like strings, lists have an index method that will return the index of a specified value. For example, to find the location in the list of the largest value:

>>> numlist = [4, 52, 33, 11, -3]
>>> numlist.index(max(numlist))
1

5.3  Methods for Sequence Types

5.3.1 Methods for All Sequence Types

There are some methods that can be used for all sequence types, such as lists, tuples, and strings. These will be demonstrated here for lists.

The count method returns the number of occurrences of an item in a list.

>>> mylist = list("monty python")
>>> print(mylist)
['m', 'o', 'n', 't', 'y', ' ', 'p', 'y', 't', 'h', 'o', 'n']

>>> mylist.count('o')
2
>>> mylist.count('x')
0

The index method returns the index of the first occurrence of an item within a list, or an error message if it is not found.

>>> mylist.index('y')
4

>>> mylist.index('x')
ValueError: 'x' is not in list


5.3.2 Methods for Mutable Sequence Types

There are methods that can be used for all mutable sequence types. They will be demonstrated here using lists.

The following methods modify the list variable.  The value that is returned is not the list, but the default value None.  These methods will be shown in a series of statements.

The append method adds one item to the end of a list.

>>> numlist = [5, 11, 33, 11, 2, -6]
>>> outval = numlist.append(44)
>>> print(numlist, outval)
[5, 11, 33, 11, 2, -6, 44] None

The insert method inserts an item into the list at the specified index. The following inserts 14 into numlist[2], and moves the rest of the items.

>>> numlist.insert(2, 14)
>>> numlist
[5, 11, 14, 33, 11, 2, -6, 44]

The extend method is used to concatenate another list to the end of the current list.

>>> numlist.extend([17, -5])
>>> numlist
[5, 11, 14, 33, 11, 2, -6, 44, 17, -5]

The result of this call to extend is the same as numlist += [17, -5].

Note that if append had been used instead of extend, the result would be a nested list ( a list in which the list [17, -5] would be the last element). This is demonstrated with a list of characters.

>>> charlist = ['x', 'q', 's']
>>> charlist.extend(['y', 'z'])
>>> charlist
['x', 'q', 's', 'y', 'z']

>>> charlist.append(['a', 'b'])
>>> charlist
['x', 'q', 's', 'y', 'z', ['a', 'b']]

The remove method can be used to remove a specified item from a list. If the item is not in the list, an error message results.

>>> numlist
[5, 11, 14, 33, 11, 2, -6, 44, 17, -5]

>>> numlist.remove(-6)
>>> numlist
[5, 11, 14, 33, 11, 2, 44, 17, -5]

>>> numlist.remove(100)
ValueError: list.remove(x): x not in list

If there are multiple occurrences of the specified item, only the first will be removed from the list.

The pop method removes an item from a specified index in a list. Unlike the previous methods, however, it returns a value (not None), which is the item that has been removed. The index can be specified using an integer. If no index is given, the default is -1 (which means the last element in the list).

>>> delval = numlist.pop(3)
>>> print(delval, 'is no longer in ', numlist)
33 is no longer in  [5, 11, 14, 11, 2, 44, 17, -5]

>>> delval = numlist.pop()
>>> print(delval, ' is no longer in ', numlist)
-5  is no longer in  [5, 11, 14, 11, 2, 44, 17]

The reverse method reverses all elements in a list; modifying the list and returning None.

>>> numlist.reverse()
>>> numlist
[17, 44, 2, 11, 14, 11, 5]

The clear method removes everything from a list, so that it becomes an empty list.

>>> numlist.clear()
>>> numlist
[]

5.3.3 List Method

In addition to the methods from the previous section, which can be used on any mutable sequence type, the list type includes a method for sorting the list, sort.  The sort method returns None, but sorts the list in place.

>>> numlist = [5, 11, 33, 11, 2, -6]
>>> numlist.sort()
>>> numlist
[-6, 2, 5, 11, 11, 33]

By default, it sorts in ascending order, (lowest to highest). This can be changed to descending order by setting the reverse flag to True in the function call:

>>> numlist.sort(reverse=True)
>>> numlist

[33, 11, 11, 5, 2, -6]

Note that there is also a built-in function in Python, sorted, which will return a new list that has been sorted, but does not sort the argument list in place.

>>> origlist = list('python')
>>> newlist = sorted(origlist)
>>> print(origlist, newlist)
['p', 'y', 't', 'h', 'o', 'n'] ['h', 'n', 'o', 'p', 't', 'y']

5.4 Range and enumerate

We have seen that the range function generates a sequence of integers and that when called as range(n), it generates the sequence of integers from 0 through n-1.  The type returned from range is range, although it can be passed to the list function if a list consisting of the individual items is desired.

>>> mr = range(6)
>>> print(mr, type(mr))
range(0, 6) <class 'range'>

>>> ml = list(mr)
>>> print(ml, type(ml))
[0, 1, 2, 3, 4, 5] <class 'list'>

So, again, range does not create a list; it creates an iterator.  An interesting aspect of iterators is that the values are created one at a time; the entire iterator is not created first.

The built-in function iter will determine whether an argument can be iterated through or not, and if so what type of iterator the argument is. For example, the range variable mr is a range iterator, a list [3, 66] is a list iterator, and an integer is not an iterator.

>>> iter(mr)
<range_iterator at 0x7f888bb480f0>

>>> iter([3, 66])
<list_iterator at 0x7f888bb48070>

>>> iter(33)
TypeError: 'int' object is not iterable

By storing the iterator object in a variable, the next function returns the next value in the iterator, e.g.

>>> imr = iter(mr)

>>> next(imr)
0
>>> next(imr)
1
>>> next(imr)
2

When there are no more values, an error message is thrown if next is called again.

If two arguments are passed to the range function, they are the first value (instead of the default of 0) and the last (minus 1).  For example, range(3,7) generates the sequence of integers 3, 4, 5, 6.

>>> mr = range(3,7)
>>> ml = list(mr)
>>> print(ml)
[3, 4, 5, 6]

An integer “step” value can also be specified as a third argument (instead of the default of 1).

>>> mr = range(3,10,2)
>>> ml = list(mr)
>>> print(ml)
[3, 5, 7, 9]

Step values can also be negative.

>>> ml = list(range(10,2,-2))
>>> print(ml)
[10, 8, 6, 4]

The range function is frequently used with for loops to specify how many times to execute the action of a loop.  More generally, the form of a for loop is

for itervar in iterator:
action

The enumerate function can be used to return both an index and an item from a sequence such as a list.

numlist = [4, 52, 33, 11, -3]
for i, item in enumerate(numlist):
print('Item', i, 'is', item)
Item 0 is 4
Item 1 is 52
Item 2 is 33
Item 3 is 11
Item 4 is -3

Notice that this gives us two iterator variables: i, which is the index, and then item, which is the value of that item in the list.



5.5 Tuples

Tuples are similar to lists, but are immutable.  Tuples are generally created by putting values in parentheses, separated by commas.

>>> mytup = (2, 11, 33)

Functions such as len and indexing/slicing work the same on tuples as on lists.

>>> len(mytup)
3

>>> mytup[1]
11

Parentheses are not always necessary:

>>> newtuple = 5, 19
>>> newtuple
(5, 19)

The concatenation operator can be used to join two tuples together.

>>> mytup + newtuple
(2, 11, 33, 5, 19)

An empty tuple is created using parentheses with nothing inside, e.g.:

>>> emptup = ()
>>> len(emptup)
0

To create a tuple with one entry, the value must be followed by a comma, and both must be in parentheses.

>>> onetup = (7,)
>>> onetup
(7,)

The parentheses and comma here are necessary. If the comma is omitted, the value is just an integer:

>>> print(type((7,)), type((7)))
<class 'tuple'> <class 'int'>

The type of a tuple is tuple, as shown.
Because of this, indexing into a tuple to get one value is not quite the same as slicing to get one value.  A slice returns another tuple, even if it only has a length of 1:

>>> mytup = (2, 11, 33)
>>> mytup[0:1]
(2,)

Indexing using 0 returns just the integer 2:

>>> mytup[0]
2

The list function can be used to create a list from a tuple:

>>> tl = list(mytup)
>>> tl
[2, 11, 33]

The tuple function can be used to create a tuple from another sequence type such as a string or a list:

>>> wordlist = ['howdy', 'hi']
>>> wordtuple = tuple(wordlist)
>>> chartuple = tuple(wordlist[0])
>>> print(wordlist, wordtuple, chartuple)
['howdy', 'hi'] ('howdy', 'hi') ('h', 'o', 'w', 'd', 'y')

Putting values into a tuple is called packing, as in:

>>> mytup = 2, 11, 33

or

>>> mytup = (2, 11, 33)

The reverse is called unpacking.  In order to unpack a tuple, it is necessary to know how many values are in the tuple and to have that many variables on the left-hand side of the assignment operator.

>>> a, b, c = mytup
>>> print(mytup, a, b, c)
(2, 11, 33) 2 11 33

Unpacking is also possible for other sequence types such as lists and strings.
5.6 For Loops and Vectorized Code

In general, in coding, for loops are used to iterate through the indices of data structures such as Python sequences in order to perform the same operation on every element. In Python, the general form of this is for a sequence seq is:

for i in range(len(seq)):
# do something with seq[i]

In Python, rather than iterating through the indices of the sequence, it is possible to iterate through the sequence itself, as in:

for item in seq:
# do something with item

Vectorizing code essentially means getting rid of loops, and instead using built-in functions and operators.

This can involve using operators such as the * concatenation operator, functions such as min, max, sum, and sorted, and methods such as count and reverse.

Another powerful way to vectorize Python code when creating lists is to use list comprehensions.

Comprehensions do not add any power to the language, but provide a convenient, succinct way to create sequences. A comprehension essentially compresses using a for loop to create and add expressions to a sequence into one line.

List comprehensions are the most common, but it is also possible to create other comprehensions.

The simplest general form of a list comprehension is
[expression for i in iterable]

which creates a list of the expressions for all values of i.  For example,

>>> [i ** 3 for i in range(5)]
[0, 1, 8, 27, 64]

This creates a list of the cubes of all values of i in the range from 0 to 4 inclusive. Assigning this to a list variable

>>> cubelist = [i**3 for i in range(5)]

is equivalent to

cubelist = []
for i in range(5):
cubelist.append(i**3)

Conditionals can be added to the list comprehension to determine which expressions based on the iterator variable to include in the list.  For example,

>>> cubelisteven = [i**3 for i in range(7) if i%2==0]

creates a list of cubes of the even integers in the range from 0 to 6 inclusive, and is equivalent to:

cubelisteven = []
for i in range(7):
if i%2 == 0:
cubelisteven.append(i**3)

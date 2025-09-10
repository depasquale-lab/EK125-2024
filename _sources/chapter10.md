Chapter 10 Introduction to NumPy and Arrays

The NumPy module is used extensively by Python programmers for mathematical and scientific computing. Most of the NumPy library is based on arrays, which are data structures that store values (elements) that are all the same type.  Typically the elements in arrays are numbers, either integers or floats. The numpy module has many built-in functions and the array objects have many associated methods for working with numbers to facilitate applications such as linear algebra and statistics.  Many data science applications work extensively with the numpy module.

Since it is a module, numpy must first be imported. It is very common to rename it as np:

>>> import numpy as np

The rest of this chapter will assume that the numpy module has been imported in this manner.

10.1 Array Basics

Arrays have dimensions. An array with one dimension is either a row or a column. Sometimes these are called vectors, either a row vector or a column vector.  Like other sequences in Python such as lists, arrays can be indexed, and the indices begin at 0.

A one dimensional array which is a row vector containing 4 elements might be depicted as:


In NumPy, the dimensions are called axes, so this is an array with one axis. We say that this is a 1 x 4 (read “1 by 4”) array; it has 1 row and 4 columns.  The length of the array is the number of elements, which is 4.

A one dimensional column vector might be depicted as:


Again, this is an array with one axis. We say that it is a 3 x 1 array; it has 3 rows and 1 column. The length of this array is 3.

Elements in a one dimensional array are found using one index.

A two dimensional array has two axes. A two dimensional array looks like a table, with both rows and columns.  For example, a 2 x 4 array (2 rows, 4 columns) might be depicted as:


The first axis is the rows, so the length of the first axis is 2. The second axis is the columns, so the length of the second axis is 4.  Two dimensional arrays have indices for both the rows and the columns, and both start at 0. Elements are indexed using two indices, the first for the row, and the second for the column.

In general, an n-dimensional array has n dimensions, or axes.  Elements are indexed using n indices. Arrays with two or more dimensions are frequently called matrices.

A scalar, which is a single value, is said to have a dimension of 0 in NumPy. Scalars are not indexed.

10.2 Creating Arrays and Subarrays

The array function and attributes of arrays:

The basic function that is used to create arrays is the function ndarray, but this function has a simpler alias called array, which we will use.  One method for creating a one dimensional array is to convert a list (or a tuple) to an array using the array function. For the rest of this chapter, we will assume that the array function has been imported.

>>> from numpy import array
>>> arr1d = array([31, 42, 11])

Note how the array is displayed by just typing the variable name and by using the print function, and note the type of the array.

>>> arr1d
array([ 31, 42, 11])

>>> print(arr1d, type(arr1d))
[31 42 11] <class 'numpy.ndarray'>

The type of the data elements can be determined using the dtype method.

>>> print(arr1d.dtype)
int64

The type int64 is an integer type that uses 64 bits to store integers.

There are several methods that return the number of dimensions, and the lengths of the axes.  The ndim method returns the number of dimensions, or in other words the number of axes.

>>> arr1d.ndim
1

The lengths of the axes are found using the shape method.

>>> arr1d.shape
(3,)

In this case, there is only one axis since it is a one-dimensional array, and the length is 3. Notice that the result is returned as a tuple.

The size of an array is the number of elements. This is always going to be a single integer.

>>> arr1d.size
3

Two dimensional arrays can be created by passing a nested list (a list of lists) to the array function. In the following example, two lists, each with 3 numbers, are used to create a 2 x 3 array.

>>> arr2d = array([[1, 3, 8], [-2, 5, 33]])
>>> print(arr2d)
[[ 1  3  8]
[-2  5 33]]

The two nested lists must have the same number of elements, so there are the same number of elements in each row of the array.  The number of dimensions is 2. The shape function returns the tuple (2, 3) since it is a 2 x 3 array, and the size (the total number of elements) is 6.

>>> arr2d.ndim
2

>>> arr2d.shape
(2, 3)

>>> arr2d.size
6




Functions and methods that create arrays:

There are quite a few ways in which arrays can be created.  Arrays can be created using a range:

>>> rgarr = array(range(5))
>>> print(rgarr)
[0 1 2 3 4]

The numpy function arange specifically creates an array using a range.

>>> rgarr = np.arange(5)
>>> print(rgarr)
[0 1 2 3 4]

Like the range function, arange can specify starting, ending, and step values.

>>> myarr = np.arange(3,9,2)
>>> print(myarr)
[3 5 7]

There are several other functions that can be used to create arrays.

The linspace function can be used to create array elements that are linearly spaced within a specified range. The following specifies that the range begins with 1, ends with 9, with 3 linearly spaced points. The linspace function determines the step value (in this case, 4). Notice that the default type returned by linspace is float64, even if the numbers are integers.

>>> myarr = np.linspace(1,9,3)
>>> print(myarr, myarr.dtype)
[1. 5. 9.] float64

If the number of elements is not specified, the default is 50. Also, the type can be specified using dtype.

>>> myarr = np.linspace(1,9,3,dtype=np.int16)
>>> print(myarr, myarr.dtype)
[1 5 9] int16

The type int16 is an integer type that uses 16 bits, so it stores smaller integers than the type int64.

An array of all zeros can be created using the zeros function, by specifying the shape. The default type of each element is float64, but like the linspace function, this can be modified using dtype.

>>> print(np.zeros((2,4), dtype=int))
[[0 0 0 0]
[0 0 0 0]]

If only one integer n is specified for the shape, a 1 x n row vector is created.

>>> zarr = np.zeros(3)
>>> print(zarr)
[0. 0. 0.]

Three dimensional arrays can be created by specifying a tuple of 3 integers for the shape. For example, a shape of (2, 3, 5) creates two 3 x 5 arrays. Notice that when displayed, the two arrays are printed separately with a blank line in between them.

>>> print(np.zeros((2,3,5), dtype=np.int16))
[[[0 0 0 0 0]
[0 0 0 0 0]
[0 0 0 0 0]]

[[0 0 0 0 0]
[0 0 0 0 0]
[0 0 0 0 0]]]

Images are often stored as three dimensional arrays.  Arrays with more than 3 dimensions can also be created, but it becomes more difficult to visualize them and to find useful applications for them.

One reason for creating an array of all zeros might be if they are going to be running sums or counters.

Arrays of all ones can be created using the ones function, which uses the same format as the zeros function.  An array of all ones might be used as a starting point for running products.

>>> print(np.ones(6, dtype=int))
[1 1 1 1 1 1]

To fill in an array with any number other than zeros or ones, the full function can be used.

>>> print(np.full((2,3), 11))
[[11 11 11]
[11 11 11]]

Instead of just a single number, a set of numbers to be used for each row can be passed to the full function, for example using range.

>>> newmat = np.full((3,4), range(4))
>>> print(newmat)
[[0 1 2 3]
[0 1 2 3]
[0 1 2 3]]

Another function that creates arrays is the empty function, which contrary to its name does not create an empty array, but fills in the elements with whatever is currently in the memory locations used for the array. This function is useful when the shape of an array is known, but the actual values in the elements will be filled in later.  Of course, your results may vary!

>>> weird = np.empty(4)
>>> print(weird)
[-2.68156159e+154 -3.11108761e+231  2.68678769e+154  2.82470694e-309]

It is frequently useful to create arrays in which random numbers are stored in the elements. NumPy has a random module that has a method, default_rng, which is used to create a random number generator. Once that has been created, the method random can be used to create random floats, and the method integers can be used to create random integers in a specified range.

An integer can be passed to default_rng which is the seed for the random number generator; if no argument is passed the seed will be obtained from the operating system.

>>> rng = np.random.default_rng()
>>> farr = rng.random(3)
>>> print(farr)
[0.74899722 0.9414599  0.70685837]

In the following example, a 1 x 4 array of random integers is created in the range from 3 to 9 inclusive.

>>> rng.integers(3,10,4)
array([9, 6, 3, 9])

Indexing and Slicing:

Arrays can be indexed and sliced similarly to Python sequences such as lists. The indices begin at 0, and negative indices allow indexing from the end of the array.

>>> arr1d = array([31, 42, 11])
>>> arr1d[1]
42

>>> arr1d[-1]
11

With two dimensional arrays, the row index is given first, and then the column index.

>>> arr2d = array([[1, 3, 8], [-2, 5, 33]])
>>> print(arr2d)
[[ 1  3  8]
[-2  5 33]]

>>> arr2d[1,2]
33

Slicing creates another array.

>>> arr1d[:]
array([31, 42, 11])

>>> arr2d[0,1:]
array([3, 8])

In addition to using integer indices, NumPy allows logical indexing.  With logical indexing, Boolean expressions resulting in True or False can be used to index into an array. This returns the elements from the array for which the corresponding element in the logical array is True.

>>> logarr = arr1d > 20
>>> logarr
array([ True,  True, False])

>>> arr1d[logarr]
array([31, 42])

Notice that for a two dimensional array, with logical indexing the resulting  array is flattened into a one dimensional array.  The elements are taken from the original array one row at a time.

>>> print(arr2d)
[[ 1  3  8]
[-2  5 33]]

>>> arr2d[arr2d > 0]
array([ 1,  3,  8,  5, 33])






Changing Dimensions:

There are NumPy methods that change the shape of an array.

The reshape method can take any array and reshape it into a new array, as long as the new array has the same number of elements as the original. For example, a 1 x 6 array could be reshaped into a 6 x 1 array, a 2 x 3 array, or a 3 x 2 array.

>>> myarr = np.arange(6)
>>> print(myarr)
[0 1 2 3 4 5]

>>> myarr.reshape(6,1)
array([[0],
[1],
[2],
[3],
[4],
[5]])

>>> arr2by3 = myarr.reshape(2,3)
>>> print(arr2by3)
[[0 1 2]
[3 4 5]]

The reshape method returns a reshaped array, but does not modify the original array. The resize method works just like reshape except that it does modify the original array.

>>> myarr = np.arange(6)
>>> myarr.resize(3,2)
>>> print(myarr)
[[0 1]
[2 3]
[4 5]]

The ravel method flattens an n-dimensional array into a one dimensional array. The default is that it flattens it one row at a time. The ravel method returns a flattened array, but does not modify the original.

>>> print(arr2by3)
[[0 1 2]
[3 4 5]]

>>> arr2by3.ravel()
array([0, 1, 2, 3, 4, 5])

>>> print(arr2by3)
[[0 1 2]
[3 4 5]]

The method named simply T transposes an array, which for a two dimensional array means that it interchanges the rows and columns. The method returns a new array, but does not modify the original. In the following example, the first row [0 1 2] becomes the first column, and the second row becomes the second column. The other way to view it is that the first column becomes the first row, the second column becomes the second row, and the third column becomes the third row.

>>> arr3by2 = arr2by3.T
>>> print(arr3by2)
[[0 3]
[1 4]
[2 5]]

Combining Arrays:

There are several functions that create new arrays by combining existing arrays.

The function vstack vertically stacks, or concatenates, arrays. A tuple consisting of the arrays to be stacked is passed to the vstack function.  In this case the one-dimensional arrays have to have the same number of elements so that the columns will match up in the stacked array.

>>> arrone = np.array([4,11,9])
>>> arrtwo = np.array([3,15,22])
>>> np.vstack((arrone, arrtwo))
array([[ 4, 11,  9],
[ 3, 15, 22]])

The function hstack horizontally stacks arrays.

>>> np.hstack((arrtwo,arrone))
array([ 3, 15, 22,  4, 11,  9])

10.3 Functions and Operations on Arrays

NumPy has functions that take arrays as arguments, and operations that can be performed on entire arrays.

Functions
NumPy has universal functions (ufuncs) to which an entire array can be passed. The function is evaluated on every element, returning an array with the same dimensions as the original.  These include trig functions such as sin, cos, tan, etc.  For example:

from math import pi
x = np.linspace(0, 2*pi, 10)
y = np.sin(x)
print(x)
print(y)

[0.      0.6981317  1.3962634  2.0943951  2.7925268  3.4906585
4.1887902  4.88692191 5.58505361 6.28318531]
[ 0.00000000e+00  6.42787610e-01  9.84807753e-01  8.66025404e-01
3.42020143e-01 -3.42020143e-01 -8.66025404e-01 -9.84807753e-01
-6.42787610e-01 -2.44929360e-16]

Other ufuncs include the square root function sqrt, the absolute value function abs, and exponential functions.  For example, we could get the absolute value of every element in a 2D array:

rng = np.random.default_rng()
nums = rng.integers(-10,10, (3,5))
print(nums)
print()
print(np.abs(nums))

[[  1  -1   7 -10   3]
[  6   2   6  -5  -3]
[ -1   1 -10  -6   9]]

[[ 1  1  7 10  3]
[ 6  2  6  5  3]
[ 1  1 10  6  9]]

There are aggregation functions that perform tasks such as summing elements, multiplying elements, and finding minimum and maximum values. By default, the aggregation is performed on the entire array, but to aggregate on just rows or columns, the axis can be specified.
For example, let’s first create a 2D array:

>>> rng = np.random.default_rng()
>>> nums = rng.integers(60, 100, (4,2))
>>> print(nums)

[[96 91]
[68 64]
[60 97]
[77 77]]

To find the overall minimum, the min function is used:

>>> np.min(nums)
60

To find the minimum for each column, specify axis 0:

>>> np.min(nums, axis = 0)
array([60, 64])

To find the minimum for each row, specify axis 1:

>>> smin = np.min(nums, axis = 1)
>>> smin
array([91, 64, 60, 77])

Other unfuncs that work the same way (overall, or specify the axis) include max, mean, median, std (standard deviation), and var (variance).

The aggregation functions also include sum and prod.  For example, to get an overall sum:

>>> rng = np.random.default_rng()
>>> nums = rng.integers(0,10, (3,4))
>>> print(nums)
[[3 9 7 3]
[1 0 2 8]
[2 0 0 1]]

>>> np.sum(nums)
36

To get a sum for every column:

>>> np.sum(nums, axis = 0)
array([ 6,  9,  9, 12])


Operations

Numerical operations can be performed on entire arrays. Scalar operations involve an array and one scalar.  For example, to add 5 to every element in an array:

>>> rowvec = array([-3, 28, 6])
>>> rowvec + 5
array([ 2, 33, 11])

Operations such as addition, subtraction, multiplication, division, and exponentiation can be performed on arrays of any dimension.  For example, to divide every element in a 2D array by 2:

rng = np.random.default_rng()
nums = rng.integers(10,20, (2,5))
print(nums)
print()
print(nums/2)

[[18 17 13 11 15]
[14 12 13 12 16]]

[[9.  8.5 6.5 5.5 7.5]
[7.  6.  6.5 6.  8. ]]

Array operations are operations that are performed element by element on two arrays that have the same dimensions.

For example, the following creates two 1 x 5 arrays, or vectors, and adds the corresponding elements to create another 1 x 5 array. This is array addition.

>>> vec1 = array([6, 2, 7, 5, 9])
>>> vec2 = array([3, 1, 4, 2, 1])
>>> vec1 + vec2
array([ 9,  3, 11,  7, 10])

Similarly, array multiplication is an element-by-element operation:

rng = np.random.default_rng()
mat1 = rng.integers(0,10, (2,3))
print(mat1)
print()
mat2 = rng.integers(0,10, (2,3))
print(mat2)
print()
print(mat1*mat2)

[[3 9 3]
[4 0 0]]

[[4 2 6]
[8 1 3]]

[[12 18 18]
[32  0  0]]

Note: this is array multiplication, not matrix multiplication.  Matrix multiplication is not performed element-by-element, and will be described in the next section.

Matrix Operations and Matrix Properties

Matrix multiplication has a very specific meaning.  By “matrix” here we are referring to 2D arrays. First of all, to multiply a matrix A by a matrix B to result in a matrix C, the number of columns of A must be the same as the number of rows of B.  If the matrix A has dimensions m x n, that means that matrix B must have dimensions n x something; called p.

The terminology is that the inner dimensions (the ns) must be the same.  The resulting matrix C has the same number of rows as A and the same number of columns as B (i.e., the outer dimensions m x p).  In mathematical notation,

[A]m x n [B]n x p = [C]m x p

This only defines the size of C, not how to find the elements of C.

The elements of the matrix C are defined as the sum of products of corresponding elements in the rows of A and columns of B, or in other words,

cij =  .

In the following example, A is 2 x 3 and B is 3 x 4; the inner dimensions are both 3, so performing the matrix multiplication A*B is possible (note that B*A would not be possible).  C will have as its size the outer dimensions 2 x 4.  The elements in C are obtained using the summation just described.  The first row of C is obtained using the first row of A and in succession the columns of B.  For example, C(1,1) is 3*1+8*4+0*0 or 35.  C(1,2) is 3*2+8*5+0*2 or 46.






A                                 B                                C
*

In NumPy, the matrix multiplication operator is @.

>>> A = array([[3, 8, 0],[1, 2, 5]])
>>> B = array([[1, 2, 3, 1], [4, 5, 1, 2], [0, 2, 3, 0]])
>>> C = A @ B
>>> print(C)

[[35 46 17 19]
[ 9 22 20  5]]

Properties of Square Matrices

A square matrix is a matrix in which the number of rows is the same as the number of columns.  The definitions that follow in this section only apply to square matrices.

The diagonal of a square matrix is the set of terms aii for which the row and column indices are the same, so from the upper left element to the lower right.  For example, for the following matrix the diagonal consists of  1,   6,  11, and   16.



A square matrix is a diagonal  matrix if all values that are not on the diagonal are 0.  The numbers on the diagonal, however, do not have to be all nonzero, although frequently they are.  Mathematically, this is written as aij = 0 for i ~= j.  The following is an example of a diagonal matrix:




The NumPy diag function can be used to create a diagonal matrix, by passing the numbers to be on the diagonal (either as a 1D array or a list).

>>> diagnums = [4, 5, 2, 7]
>>> np.diag(diagnums)

array([[4, 0, 0, 0],
[0, 5, 0, 0],
[0, 0, 2, 0],
[0, 0, 0, 7]])

If instead a diagonal matrix is passed to the diag function, it returns the diagonal as a 1D array.

>>> myd = np.diag([33, 2, 11])
>>> np.diag(myd)
array([33,  2, 11])

So, the diag function can be used two ways: (i) pass a matrix and it returns a vector, or (ii) pass a vector and it returns a matrix!

A square matrix is an identity matrix called I if aij = 1 for i == j and aij = 0 for i ~= j.  In other words, all of the numbers on the diagonal are 1 and all others are 0.  The following is a 3 x 3 identity matrix:



Note that any identity matrix is a special case of a diagonal matrix.

Identity matrices are very important and useful.  NumPy has a built-in function eye that will create an n x n identity matrix, given the value of n:

>>> np.eye(4)
array([[1., 0., 0., 0.],
[0., 1., 0., 0.],
[0., 0., 1., 0.],
[0., 0., 0., 1.]])

A square matrix is symmetric if aij = aji for all i, j.  In other words, all of the values opposite the diagonal from each other must be equal to each other.  In this example, there are three pairs of values opposite the diagonals, all of which are equal (the 2s, the 9s, and the 4s).



10.4 Assigning and Copying Array Variables

NumPy arrays contain the actual data, and also metadata such as the data type.

Since array variables are mutable, assigning one array variable to another works like lists. No new object is created.

>>> vec1 = array([6, 2, 7, 5, 9])
>>> vec2 = vec1
>>> vec2 is vec1
True

So, changing one variable changes the other since they are both referring to the same array.

>>> vec1[2] = 11
>>> print(vec1)
>>> print(vec2)

[ 6  2 11  5  9]
[ 6  2 11  5  9]

Assigning a new array to either of the variables creates a completely new location.

>>> vec1 = np.arange(2,6)
>>> print(vec1)
>>> print(vec2)

[2 3 4 5]
[ 6  2 11  5  9]

If it is desired to have two array variables store the same values, but not to refer to the same lo-cation, the copy function can be used instead of the assignment operator.

This creates what is called a deep copy, and copies all of the metadata.

>>> vec1 = array([6, 2, 7, 5, 9])
>>> vec2 = np.copy(vec1)
>>> vec2 is vec1
False

Dictionaries and Intro to Pandas

Pandas is a data manipulation library that is built on NumPy. The basic Pandas data structures are Series and DataFrames. Series are essentially one-dimensional arrays and DataFrames are two-dimensional arrays, but the row and/or columns can be labeled.  Frequently DataFrames are created by reading in data from a csv (comma separated value) file or spreadsheet file, but they can also be created programmatically which is what we will focus on here. Python dictionaries are commonly used to create Series and DataFrames. In this section, we will first introduce dictionaries, and then in an introduction to Pandas, will use dictionaries to create Series and DataFrames.

Dictionaries

Dictionaries are a Python data structure, but they are a mapping type, not a sequence.  This is because indexing into a dictionary is accomplished using keys, not integers. The type of a dictionary is dict.

Dictionaries are created by putting key-value pairs in curly braces. Keys are names specified as strings. The pair is specified as a key followed by a colon, followed by the value for that key, as in ‘key’:value.  The following is an example of a dictionary that stores information about a particular hurricane.

>>> bigone = {'name':'Bertha', 'year': 1952, 'category': 4}

Values can be retrieved from a dictionary by giving the name of the dictionary variable and then the name of the key in square brackets.

>>> bigone['year']
1952

An error will result if the key does not exist in the dictionary.

>>> bigone['size']

KeyError: 'size'

An error will also occur if you try to index using an integer; values are only referenced using keys.

Dictionaries are a mutable type. Values can be modified using assignment statements.

>>> bigone['category'] = 5
>>> bigone
{'name': 'Bertha', 'year': 1952, 'category': 5}
More key-value pairs can be added to a dictionary in the same way.

>>> bigone['eyewidth'] = 400
>>> bigone
{'name': 'Bertha', 'year': 1952, 'category': 5, 'eyewidth': 400}

Key-value pairs can be deleted from a dictionary using the del command.

>>> del bigone['eyewidth']
>>> bigone
{'name': 'Bertha', 'year': 1952, 'category': 5}

The len function returns the number of key-value pairs in the dictionary.

>>> len(bigone)
3

The in and not in operators can be used to find whether a key is in a dictionary or not.

>>> 'year' in bigone
True

>>> 'sqarea' not in bigone
True

The list function will return a list of all of the key names from a dictionary.

>>> list(bigone)
['name', 'year', 'category']

There are a number of methods that work with dictionaries.

The get method retrieves a value from a dictionary; it returns None by default if the key is not in the dictionary.

>>> bigone.get('year')
1952

If the key is not in the dictionary, the value None that is returned is not automatically shown, but can be printed, or tested in a selection statement.

>>> print(bigone.get('size'))
None

A value other than None can also be specified to be used if the key is not in the dictionary, e.g. a flag value of -999.

>>> bigone.get('size', -999)
-999

Note that this does not add a key-value pair to the dictionary.

The get method is therefore safer to use than just putting a key name in square brackets, since get will return a value if the key is not found, whereas using square brackets will result in an error if the key is not found.

The pop method deletes an item from a dictionary and returns its value. A default value to return can be specified in case the key is not in the dictionary; if the default is not specified and the key is not found in the dictionary, an error results.

>>> delcat = bigone.pop('category')
>>> delcat
5

>>> bigone
{'name': 'Bertha', 'year': 1952}

>>> bigone.pop('size')
KeyError: 'size'

>>> bigone.pop('size', -999)
-999

The popitem method deletes the last key-value pair in a dictionary, and returns this as a tuple.

>>> k,v = bigone.popitem()
>>> print(k,v)
year 1952

The clear method deletes all of the key-value pairs from a dictionary.

>>> bigone.clear()
>>> bigone
{}

There are also methods that can be used to iterate: keys(), values(), and items(), for the dictionary’s keys, values, and key-value pairs, respectively.

For example, the following call to the keys method returns the names of the keys. Technically, it returns a view object, dict_keys.

>>> bigone = {'name':'Bertha', 'year': 1952, 'category': 4}
>>> bigone.keys()
dict_keys(['name', 'year', 'category'])

Normally, the view object would not be accessed or displayed, however. Instead, it would be typical to iterate over the result.

for kname in bigone.keys():
print('The key is', kname)
The key is name
The key is year
The key is category

To loop over the key-value pairs, the items method is used, and two iterator variables are created to store the keys and values individually.

for k, v in bigone.items():
print('The value of',repr(k),'is',v)
The value of 'name' is Bertha
The value of 'year' is 1952
The value of 'category' is 4

We have stored information about one hurricane in a dictionary.  In order to store information on more than one hurricane, we could create a list of dictionaries.

>>> hurr0 = {'name': 'Bertha', 'year': 1952, 'category': 4}
>>> hurr1 = {'name': 'Bob', 'year': 1990, 'category': 2}
>>> hurr2 = {'name': 'Camilla', 'year': 1960, 'category': 5}
>>> hurricanes = [hurr0, hurr1, hurr2]
>>> hurricanes[2]  # show example
{'name': 'Camilla', 'year': 1960, 'category': 5}

Once we have a list of dictionaries, we could iterate through the list, for example to print information on the more powerful hurricanes.

print('The largest hurricanes were:')
for hurr in hurricanes:
if hurr['category'] >= 4:
print(repr(hurr['name']))
The largest hurricanes were:
'Bertha'
'Camilla'
It is also possible for values in a dictionary to be data structures themselves. This has already been done, since strings are a sequence data type. Another possibility would be to have a list as a value.  Note also in this example that each key-value pair is entered on a separate line, which makes it easier to read.

icdessert = {
'flavor': 'malted',
'cone': True,
'nscoops': 2,
'addins': ['pecans', 'chocolate chips']
}
icdessert['addins']
['pecans', 'chocolate chips']

Since the key 'addins' is a list, it can be indexed.

>>> icdessert['addins'][0]
'pecans'

We could use a for loop to print the elements from the list individually.

print('Your ice cream add-ins are:')
for yummy in icdessert['addins']:
print(yummy.title(),'!!!')
Your ice cream add-ins are:
Pecans !!!
Chocolate Chips !!!

For a dictionary comprehension,  key-value pairs must be created.

>>> cubedict = {i: i**3 for i in range(5)}
>>> cubedict
{0: 0, 1: 1, 2: 8, 3: 27, 4: 64}


Introduction to Pandas

Since Pandas is built on NumPy, they are frequently imported together using the following:

>>> import numpy as np
>>> import pandas as pd

The rest of this section will assume that these have been imported.


Series

A Pandas Series is a one-dimensional array that can be created using a list or an array. For example,

>>> numseries = pd.Series([11, 33, 15, 2])
>>> numseries
0    11
1    33
2    15
3     2
dtype: int64

Notice that the indices are explicitly listed as part of the Series (which must be capitalized) and that the dtype is also stored in the variable and displayed.

The numbers can be accessed using values:

>>> numseries.values
array([11, 33, 15,  2])

You can see that it is stored as a NumPy array.  You can index into the Series and slice it, just like in Python and NumPy.

>>> numseries[0]
11

>>> numseries[1:3]
1    33
2    15
dtype: int64

The indices can be accessed using index, although the result might not be what you would expect!

>>> numseries.index
RangeIndex(start=0, stop=4, step=1)

From this you can see that the indices are a range beginning at 0. Indices can also be specified.

>>> numlabels = pd.Series([11, 33, 15, 2], ['a','b','c','d'])
>>> numlabels
a    11
b    33
c    15
d     2
dtype: int64
The labels can then be used to index and slice into the Series.

>>> numlabels['c']
15

>>> numlabels['b':'d']
b    33
c    15
d     2
dtype: int64

Implicit integer indices can also be used to index and to slice into the Series. Notice, however, that using 'b':'d' returns 3 rows, whereas [1:3] only returns 2 (like Python and NumPy).

>>> numlabels[1:3]
b    33
c    15
dtype: int64

A Series can also be created using a dictionary.

>>> numdict = {'a':11, 'b':33, 'c':15, 'd':2}
>>> numlab = pd.Series(numdict)
>>> numlab
a    11
b    33
c    15
d     2
dtype: int64


DataFrames

A Pandas DataFrame looks like a two-dimensional array with labels for the rows and the columns. A DataFrame can be constructed from a single Series, for example from above:

>>> nl = pd.DataFrame(numlab,columns = ['Nums'])
>>> nl


DataFrames usually have multiple columns, however.

Let’s create a DataFrame with information on students by constructing multiple Series using dictionaries.
id_dict = {'Joey': 123, 'Javier': 234, 'Juanita': 456, 'Jane': 678}
ids = pd.Series(id_dict)
exam1_dict = {'Joey': 95, 'Javier': 99, 'Juanita': 88, 'Jane': 100}
exam1s = pd.Series(exam1_dict)
students = pd.DataFrame({'ID': ids, 'Exam1': exam1s})
students

The index attribute shows the indices, which are in an Index object that stores the row labels.

>>> students.index
Index(['Joey', 'Javier', 'Juanita', 'Jane'], dtype='object')

The columns attribute shows the indices, which are in an Index object that stores the column labels.

>>> students.columns
Index(['ID', 'Exam1'], dtype='object')

The values attribute returns the numbers in the two columns as a 2D array.

>>> students.values
array([[123,  95],
[234,  99],
[456,  88],
[678, 100]])

In order to access a column in the DataFrame, the column name can be specified in two ways:

>>> idcol = students['ID']
>>> idcol
Joey       123
Javier     234
Juanita    456
Jane       678
Name: ID, dtype: int64
>>> idcol = students.ID
>>> idcol
Joey       123
Javier     234
Juanita    456
Jane       678
Name: ID, dtype: int64

Note that this is a Series. Then, to access an individual Id from the Series, we can index using the implicit integer index or using the row label.

>>> idcol[0]
123

>>> idcol['Javier']
234

Of course, it is not necessary to extract the column first before indexing to get an individual value. These can be combined.

>>> students.ID[0]
123

>>> students['ID']['Jane']
678

In order to access a row in a DataFrame, the iloc method can be used with an implicit index, or the loc method can be used with a label.

>>> students.loc['Juanita']
ID       456
Exam1     88
Name: Juanita, dtype: int64

>>> students.iloc[2]
ID       456
Exam1     88
Name: Juanita, dtype: int64

Note that this is a Series.

There are several functions and methods that can be used to find the dimensions of a DataFrame. The len function can be used to find the number of rows, and by specifying .columns the number of columns.

>>> len(students)
4
>>> len(students.columns)
2

The shape method will return both dimensions as a tuple.

>>> students.shape
(4, 2)

A column can be added to the DataFrame as follows:

>>> students['Exam2'] = [100, 99, 98, 97]
>>> students

Column(s) can be deleted using the drop method. This must be assigned to the DataFrame object.

>>> students = students.drop(columns = 'ID')
>>> students

Statistical methods that can be used include mean(), sum(), min(), max(), std(), and var(). They can be used with the entire DataFrame, or an individual column.
>>> students.mean()
Exam1    95.5
Exam2    98.5
dtype: float64

If a DataFrame object is large, which it frequently will be if read from a file, the first 5 rows can be viewed using the head() method, and the last 5 rows can be viewed using the tail() method.
Scalar operations

Scalar operations can be performed on arrays (vectors or matrices).  For example, one can perform scalar operations on the following vector vec:

>> vec = 1: 0.5: 3
vec =
1.0000    1.5000    2.0000    2.5000    3.0000

Multiplying the vector by 2 performs the multiplication on every element in the vector, resulting in a vector with the same length as the original. Since this is not stored in a variable, the result is stored in the default variable ans.

>> vec * 2
ans =
2     3     4     5     6

All numerical operators can be used in this way. For example, we can add 5 to every element:

>> newv = vec + 5
newv =
6.0000    6.5000    7.0000    7.5000    8.0000

Scalar operations can also be performed on matrices.

>> mat = randi([5, 20], 2, 3)
mat =
17    15    18
20     5    19
>> mat / 2
ans =
8.5000    7.5000    9.0000
10.0000    2.5000    9.5000

Array operations

Array operations are operations that are performed on corresponding elements of two arrays, so they must have the same dimensions.

>> vec1 = [2 11 33 5];
>> vec2 = linspace(3, 9, 4)
vec2 =
3     5     7     9
>> vec1 + vec2
ans =
5    16    40    14

For operations that are based on multiplication, the operator must have a dot in front of it.  So, the multiplication array operators are:
.^
.*
./
.\

>> vec2
vec2 =
3     5     7     9
>> vec2 .^ 2
ans =
9    25    49    81

>> mata = [1 3; 2 1]
mata =
1     3
2     1
>> matb = [4 2; 1 5]
matb =
4     2
1     5
>> mata .* matb
ans =
4     6
2     5

Matrix multiplication

So, .* is array multiplication. The matrix multiplication operator is just *.

>> matc = mata * matb
matc =
7    17
9     9

Logical operators

Logical operators can be used with arrays, also.

>> vec = randi([1,20], 1,5)
vec =
16    15     8    14     4
>> isless10 = vec < 10
isless10 =
1x5  array
0   0   1   0   1
Logical indexing also works in MATLAB.

>> vec(isless10)
ans =
8     4

>> vec == vec
ans =
1x5  array
1   1   1   1   1

To find out just true/false whether two vectors are equal to each other, use isequal.

>> isequal(vec, vec)
ans =

1

Arrays as Function Arguments

Entire arrays can be passed to functions. The function will evaluate each of the elements in the array and return an array with the same dimensions as the original.

>> myvec = [-3: 2]
myvec =
-3    -2    -1     0     1     2
>> abs(myvec)
ans =
3     2     1     0     1     2

>> mymat = randi([0, 5], 2, 4)
mymat =
0     5     3     4
2     2     1     1
>> sqrt(mymat)
ans =
0    2.2361    1.7321    2.0000
1.4142    1.4142    1.0000    1.0000

>> x = linspace(-2*pi, 2*pi, 6);
>> y = sin(x)
y =
0.0000    0.5878   -0.9511    0.9511   -0.5878   -0.0000

Functions that change array dimensions

The reshape function can change the dimensions of any array to any other array that has the same number of elements.

>> ranmat = randi([1,20], 2,4)
ranmat =
9    16    14    17
19    20     1    19
>> reshape(ranmat,4,2)
ans =
9    14
19     1
16    17
20    19

The rot90 function rotates a matrix 90 degrees counterclockwise.

>> ranmat
ranmat =
9    16    14    17
19    20     1    19
>> rot90(ranmat)
ans =
17    19
14     1
16    20
9    19

There are several functions that flip matrices.  The fliplr function flips a row vector or the columns of a matrix from left to right.

>> vec = 2:3:14
vec =
2     5     8    11    14
>> fliplr(vec)
ans =
14    11     8     5     2

The flipud function flips a column vector or the rows of a matrix up to down.

>> vec = 2:3:14
vec =
2     5     8    11    14
>> fliplr(vec)
ans =
14    11     8     5     2

The flip function flips a row vector left to right or a column vector or matrix up to down.

There are functions that replicate a matrix or element from a matrix. The repmat function replicates an entire matrix.  The following replicates a matrix variable mymat 6 times, as a 2 x 3 matrix of mymats.

>> mymat = [1 2; 3 4]
mymat =
1     2
3     4
>> repmat(mymat,2,3)
ans =
1     2     1     2     1     2
3     4     3     4     3     4
1     2     1     2     1     2
3     4     3     4     3     4

The repelem function replicates each element, in this case as a 2 x 3 matrix of each element.

>> mymat = [1 2; 3 4]
mymat =
1     2
3     4
>> repelem(mymat, 2,3)
ans =
1     1     1     2     2     2
1     1     1     2     2     2
3     3     3     4     4     4
3     3     3     4     4     4

Array Functions and Statistical Functions

There are functions that perform statistical analyses on vectors, including:
min: minimum value
max: maximum value
mean: average
mode: number that appears most frequently
median: number in the middle of a sorted vector
std: standard deviation
var: variance
sum: sum

For example,

>> vec = [5 33 11 2 7 9 4]
vec =
5    33    11     2     7     9     4
>> min(vec)
ans =
2
>> mean(vec)
ans =
10.1429

For matrices, all of these functions work column-wise:

>> mat = randi([1, 10], 3, 5)
mat =
4     4     7     7     1
2     6     3     8     3
8     2     7     5    10
>> max(mat)
ans =
8     6     7     8    10
>> sum(mat)
ans =
14    12    17    20    14

So, notice that the result is a row vector that contains the result of the function for each column.  To get an overall, for example overall maximum, get the max of this row vector:

>> max(max(mat))
ans =
10
>> sum(sum(mat))
ans =
77

Other similar functions include:
prod: product
cumsum: cumulative sum
cumprod: cumulative product
cummin: cumulative minimum
cummax: cumulative maximum

These can similarly work on a vector or the columns of a matrix.

>> rvec = 2:5
rvec =
2     3     4     5
>> prod(rvec)
ans =
120
>> rvec = [rvec 11]
rvec =
2     3     4     5    11


>> cumsum(rvec)
ans =
2     5     9    14    25

>> mat = randi([0,5], 3, 4)
mat =
0     4     3     1
1     3     1     4
3     2     4     1
>> prod(mat)
ans =
0    24    12     4
>> cummin(mat)
ans =
0     4     3     1
0     3     1     1
0     2     1     1

The diff function returns differences between consecutive elements in a vector.

>> vec = [5 33 11 2 7]
vec =
5    33    11     2     7
>> diff(vec)
ans =
28   -22    -9     5

Note that the result has one fewer element than the original vector.

The sort function sorts a vector, or columns of a matrix.

>> mat
mat =
0     4     3     1
1     3     1     4
3     2     4     1
>> sort(mat)
ans =
0     2     1     1
1     3     3     1
3     4     4     4


Square Matrices

There are functions that operate on square matrices. The diag function returns the diagonal of a matrix, or creates a diagonal matrix by putting a vector on the diagonal.

>> mydm = diag([2:4])
mydm =
2     0     0
0     3     0
0     0     4
>> diag(mydm)
ans =
2
3
4

The trace of a square matrix is the sum of the diagonal; the trace function will return this.

>> trace(mydm)
ans =
9

The eye function creates an Identity matrix.

>> eye(4)
ans =
1     0     0     0
0     1     0     0
0     0     1     0
0     0     0     1

There are “is” functions that ask True/False questions about square matrices.  The isdiag function returns 1 for true if a matrix is a diagonal matrix.

>> isdiag(mydm)
ans =
logical
1

The issymmetric function returns logical 1 if the matrix is a symmetric matrix.

>> smat = [1 2 3; 2 7 4; 3 4 5]
smat =
1     2     3
2     7     4
3     4     5
>> issymmetric(smat)
ans =
logical
1

Input

Input into a MATLAB program is achieved using the input function.  A character vector, which is the prompt, is passed, and the user’s input should be stored in a variable. For example, to read in a number:

>> favnum = input('Please enter your fave num: ')
Please enter your fave num: 33
favnum =
33

The user could also be prompted for a vector, but would have to know the proper syntax.

>> urvec = input('Enter a vector: ')
Enter a vector: [4 8 2 9]
urvec =
4     8     2     9

>> urvec = input('Enter a vector: ')
Enter a vector: 4:5:25
urvec =
4     9    14    19    24

If the user is to enter a character or a character vector, a second argument is passed to the input function, 's'.

>> favpunct = input('Enter your fave punctuation mark: ', 's')
Enter your fave punctuation mark: !
favpunct =
'!'

>> icolor = input('What is your eye color: ', 's')
What is your eye color: brown
icolor =
'brown'

It is not possible to read directly into a string variable. However, a character vector can be converted to a string.

>> stricolor = string(icolor)
stricolor =
"brown"

The input function can only read in one thing at a time. Multiple desired inputs means multiple calls to the input function. (Note that a vector is considered one thing.)


Output

MATLAB has two basic output functions: disp and fprintf.  The disp function is a quick way of displaying an expression, but it does not allow any formatting. It does, however, always print a newline character at the end. The fprintf function allows custom formatting of the output. Vectors and matrices are best displayed using disp.

Here are some examples using disp:

>> disp(4e2)
400

>> disp('Hi there!')
Hi there!

>> disp("Hello")
Hello

>> disp(3:7)
3     4     5     6     7

>> disp(eye(3))
1     0     0
0     1     0
0     0     1

The fprintf function allows formatting. For example, the following prints the number 33 in a sentence. Two arguments are passed to the fprintf function: a format string, and the number 33. The %d in the format string is a place holder, meaning that whatever comes after the format string fills in in that location.  The newline character \n at the end moves the cursor down.

>> fprintf('The number is %d.\n', 33)
The number is 33.
>>

Without the newline character, the next prompt would end up on the same line as what was printed. It’s still a prompt, but it looks messy!

>> fprintf('The number is %d.', 33)
The number is 33.>> 5 - 2
ans =
3

The basic place holders are %d for integers (decimal integers), %f for floats, %c for single characters, and %s for character vectors or strings.  The format string can be either a character vector or a string.

>> fprintf("The character is '%c'!!\n", 'x')
The character is 'x'!!

>> fprintf("The word is %s!!\n", 'fun')
The word is fun!!

>> fprintf('The word is "%s"!!\n', "fun")
The word is "fun"!!

>> fprintf('The number is %f, I think.\n', 11.11)
The number is 11.110000, I think.

The field width, number of decimal places (for floats) and justification can be specified.

The field width can be specified by putting an integer in between the % and the character in the place holder. For example, to print an integer in a field width of 5:

>> fprintf('The number is %5d!!\n', 33)
The number is    33!!

A negative integer will left-justify instead of right.

>> fprintf('The number is %-5d!!\n', 33)
The number is 33   !!

For floats, the number of decimal places can be specified. For example, a place holder of %6.2f prints in a field width of 6 altogether, including the decimal point and 2 decimal places, so in the format xxx.xx.

>> fprintf('The real number is %6.2f!!\n', 12.3)
The real number is  12.30!!

The field width does not need to be specified. If just the number of decimal places is specified, the field width will be set according to how wide the actual number is.  For example,

>> fprintf('The cost was $%.2f, wow.\n', 123.456)
The cost was $123.46, wow.

If more than one expression is to be printed, there will be multiple place holders in the format string.

>> fprintf('Int: %d, Char: %c\n', 33, 'x')
Int: 33, Char: x




Scripts

We have seen that commands, statements, and expressions can be entered interactively one at a time in the Command Window. It is also possible to group them together into a script, and then have MATLAB execute the statements in the script sequentially. From the Home tab, you can click on the “New Script” icon, which will bring up a new Editor window. Once the statements have been entered in the Editor, from the Editor tab, you can click on Save to save the file. Code files including simple scripts are stored in files with the extension of .m on the name.

For example, the following was entered in the Editor, and saved in a file named ‘myscript1.m’.

myscript1.m
% This script calculates and prints the area of a rectangle
disp('Enter the length and width of a rectangle in inches.')
rlength = input('Enter the length: ');
rwidth = input('Enter the width: ');
fprintf('The area is %.2f\n', rlength * rwidth)

The first line in the file is a comment. Comments are anything from a % to the end of that line.

To execute the script, type the name of the code file (without the .m) at the prompt in the Command Window.

>> myscript1
Enter the length and width of a rectangle in inches.
Enter the length: 4.2
Enter the width: 3.3
The area is 13.86

To view the script from the Command Window, the type command can be used.

>> type myscript1

% This script calculates and prints the area of a rectangle
disp('Enter the length and width of a rectangle in inches.')
rlength = input('Enter the length: ');
rwidth = input('Enter the width: ');
fprintf('The area is %.2f\n', rlength * rwidth)

Selection Statements

There are several selection statements in MATLAB, including the if statement, if-else statement (with optional elseif clause), and the switch statement.

The if statement chooses whether an action is executed or not. The general form is:
if condition
action
end

The condition is a Boolean expression that is either true or false. If the condition is true, the action is executed – otherwise it is not executed. The action can be any number of statements up to the key word end.  The action should be indented to make it easy to see.

For example, if a number should be positive, an if statement would change it if it is negative.
if num < 0
num = abs(num);
end

The if-else statement chooses between two actions.  The general form is:

if condition
action1
else
action2
end

Again, the condition is a Boolean expression. If the value of the condition is true, the first action (action1) is executed. If instead the condition is false, the second action (action2) is executed. The actions are naturally bracketed by the reserved words else and end.  One, and only one, of the actions will be executed. Which one depends on the value of the condition.

For example,

rint = randi([1, 10]);
if rint <= 5
fprintf('Lower half\n')
else
fprintf('Upper half\n')
end

If multiple actions are desired based on multiple conditions, nested if-else statements can be used with the optional elseif clause.  The general form is:

if condition1
action1
elseif condition2
action2
elseif condition3
action3
else  % can have many more elseif
actionn
end

The switch statement is used when you want to test a variable to see whether it is equal to different values, with different actions for each. For example, if you have a variable x and want to see whether it is equal to a, b, or c, the code could be written using an if-else statement, or a switch statement.  The algorithms would be:



if x == a
action1
elseif x == b
action2
elseif x == c
action3
else
action4
end



switch x
case a
action1
case b
action2
case c
action3
otherwise
action4
end

The switch statement has case labels; the value of the variable is compared to the values on the case labels. If none of them are equal, the otherwise clause handles “none of the above”.

The switch statement does not add any power to the language, but may be easier to read.

One application of the switch statement is to choose different actions from a menu. MATLAB has a menu function that graphically presents the user with options.

For example, the following menu function asks the user to choose a color.

>> choice = menu('Choose a color', 'red', 'green', 'blue')

This brings up a box in that looks like this:




The first character vector passed to menu is a prompt that appears at the top. The others are labels that go on buttons. If the user pushes the first button (labeled ‘red’), the value returned from the menu function is 1, if the user pushes the second button the value returned is 2, if the user pushes the third button the value is 3, and if the user pushes the red circle, the value returned is 0.  Once the value is returned and stored in the variable choice, a switch statement could then do different actions based on the user’s choice.

choice = menu('Choose a color', 'red', 'green', 'blue')
switch(choice)
case 1
fprintf('Your chose red!')
case 2
fprintf('You chose green!')
case 3
fprintf('You chose blue!')
otherwise
fprintf('Sadly, you made no choice.')
end

Instead of the otherwise clause, in this example a case label of 0 could be used.

Simple Plots

There are many simple plot types in MATLAB. Creating and annotating a plot is generally an iterative process, until the plot looks the way you want it to. For this reason, it is usually easiest to write a script to create a plot rather than doing it one line at a time in the Command Window.

To begin, create vectors storing the data points. Plots can be created programmatically, as in the following. This creates an x vector ranging from -pi to 2pi, using linspace which will by default create 100 elements. The y vector is sin(x). Both assignments are suppressed. Then, the plot function plots the vectors as points using the color blue and the marker ‘*’. The plot is then annotated with labels on the x and y axes and a title on top.



x = linspace(-pi, 2*pi);
y = sin(x);
plot(x,y, 'b*')
xlabel('x')
ylabel('sin(x)')
title('sin(x) from -pi to 2pi')

This brings up a Figure Window that contains the following plot.


The plot can be modified from the Figure Window, for example under Insert you can insert x and y axis labels and a title directly on the plot.

It is also possible to create plots without using the functions. You can choose variables in the Workspace Window, and then under the Plots tab you can click on a plot type.

Loops

In general in programming, there are two kinds of loops: counted loops, that repeat an action a specified number of times, and conditional loops, that repeat an action until something happens or as long as a condition is true. In MATLAB, the for loop is the counted loop, and while is the conditional loop.

For loop:

The general form of a for loop is

for loopvar = range
action
end

where loopvar is the loop variable, range is the range through which it iterates, and action is the set of statements that will be repeated.  Frequently the colon operator is used to specify the range.  For example, a loop to repeat 5 times would have the form:

for i = 1:5
action
end

This specifies that the loop variable i iterates through the integers from 1 to 5, so the action is repeated 5 times.

Sometimes the loop variable is used in the action, and sometimes it is not (it is just used to specify how many times to repeat the action). For example, the following uses the value of i:

for i = 3:-1 :1
disp(i)
end
3
2
1

The following does not use the loop variable in the action:

for i = 1:4
fprintf('!')
end
!!!!

The loop variable can be used to index into a vector variable.

vec = [33 11 2 5];
for i = 1:length(vec)
fprintf('%d: %d\n', i, vec(i))
end
1: 33
2: 11
3: 2
4: 5

If a vector is to be created in a loop, it is best practice to preallocate the vector first if the eventual length of the vector is known. Vectors can be extended, but that is very inefficient. It is common to preallocate a vector to all zeros.  For example:

>> vec = zeros(1,3);
>> for i = 1:3
vec(i) = input('Enter a number: ');
end
Enter a number: 4
Enter a number: 9
Enter a number: 2
>> vec
vec =
4     9     2

While loops

The conditional loop in MATLAB is the while loop. The general form is:

while condition
action
end

The condition is a Boolean expression. The action is repeated as long as the condition is true. The indentation of the action is not necessary, but makes it easier to read. The action is any number of statements up to the reserved word end.

For example, the following loops to prompt the user for a number greater than 50, until the user does this.

num = input('Enter a number > 50: ');
while num <= 50
num = input('Enter a number > 50: ');
end
fprintf('Thanks, you entered %.1f\n', num)

Enter a number > 50: 33
Enter a number > 50: -8
Enter a number > 50: 52
Thanks, you entered 52.0





Nested loops

A nested loop is one loop inside the action of another loop.  For example, a nested for loop to print might look like this:

for i = 1:3
for j = 1:5
fprintf('*')
end
fprintf('\n')
end
*****
*****
*****

In the following example, the script prompts the user for 3 negative numbers to store in a vector, each time looping to error-check until the user enters a negative number.

createnvec.m
negvec = zeros(1,3);
for i = 1:3
num = input('Enter a negative number: ');
while num >= 0
num = input('Enter a negative number: ');
end
negvec(i) = num;
end
disp(negvec)

Here is an example of executing the script:

>> createnvec
Enter a negative number: -4
Enter a negative number: 33
Enter a negative number: 2
Enter a negative number: -7
Enter a negative number: -11
-4    -7   -11

Nested loops can also be used to perform an operation on every element in a matrix. One loop would be over the rows of the matrix, and the other loop over the columns.

For example, given a matrix variable mat, we will write code to find the overall sum of the numbers in the matrix, the sum of each row, and the sum of each column (without using the sum function).





matsums.m
mat = [1 3 5; 2 6 3]
[r c] = size(mat);

% Calculate the overall sum
mysum = 0;
for i = 1:r
for j = 1:c
mysum = mysum + mat(i,j);
end
end
fprintf('The overall sum is %d.\n\n', mysum)

% Calculate the sum for each row
for i = 1:r
mysum = 0;
for j = 1:c
mysum = mysum + mat(i,j);
end
fprintf('Sum for row %d: %d\n', i, mysum)
end
fprintf('\n')

% Calculate the sum for each column
for j = 1:c
mysum = 0;
for i = 1:r
mysum = mysum + mat(i,j);
end
fprintf('Sum for column %d: %d\n', j, mysum)
end

Executing this would result in:

>> matsums
mat =
1     3     5
2     6     3
The overall sum is 20.

Sum for row 1: 9
Sum for row 2: 11

Sum for column 1: 3
Sum for column 2: 9
Sum for column 3: 8




There are several things to note in this code:
When a result is calculated for every row, the outer loop has to be over the rows
When a result is calculated for every column, the outer loop has to be over the columns
When an overall result is calculated, it does not matter whether the outer loop is over the rows or columns
The matrix is always indexed with the row index first, then the column index, regardless of the order of the loops
For an overall sum, the running sum variable is initialized to 0 before the nested loop
For a sum of every row, the running sum variable must be initialized to 0 for every row
For a sum of every column, the running sum variable must be initialized to 0 for every column


Vectorizing Code

Since MATLAB is written to work with vectors and matrices, it is never necessary to use loops when performing an operation on every element in a vector or matrix, or to call a function on every element in a vector or matrix.

For example, to add 5 to every element in a vector we could loop as follows:

>> vec = [4 9 2];
>> for i = 1:length(vec)
vec(i) = vec(i) + 5;
end
>> vec
vec =
9    14     7

The vectorized code would be instead:

>> vec = [4 9 2];
>> vec = vec + 5
vec =
9    14     7

Similarly, to multiply every element in a matrix by 2, we could use a nested loop as follows:

>> mat = [3:5; 2 11 16]
mat =
3     4     5
2    11    16
>> [r c] = size(mat);
>> for i = 1:r
for j = 1:c
mat(i,j) = mat(i,j) * 2;
end
end


>> mat
mat =
6     8    10
4    22    32

The vectorized code is:

>> mat = [3:5; 2 11 16]
mat =
3     4     5
2    11    16
>> mat = mat * 2
mat =
6     8    10
4    22    32

User-Defined functions

We will categorize functions as follows:
Functions that calculate and return one value
Functions that calculate and return more than one value
Functions that just accomplish a task, such as printing, without returning any values

Thus, although many functions calculate and return values, some do not.  Instead, some functions just accomplish a task.  There are differences between these three types of functions, including the format of the function headers and also the way in which the functions are called. Regardless of what kind of function it is, all functions must be defined, and all function definitions consist of the header and the body.  Also, the function must be called for it to be utilized.  Although functions can be stored in script code files, for now we will concentrate on functions that are stored in their own code files with an extension of .m.

In general, any function in MATLAB consists of the following:
The function header (the first line); this has:
the reserved word function
if the function returns values, the name(s) of the output argument(s), followed by the assignment operator (=)
the name of the function (important: this should be the same as the name of the file in which this function is stored to avoid confusion)
the input arguments in parentheses, if there are any (separated by commas if there is more than one).
A comment that describes what the function does (this is printed if help is used).
The body of the function, which includes all statements, including putting values in all output arguments if there are any.
end at the end of the function.

User-defined functions that return a single value

The general form of a function definition for a function that calculates and returns one value looks like this:

functionname.m
function outputargument = functionname(input arguments)
% Comment describing the function

Statements here; these must include putting a value in the output argument

end % of the function

For example, the following is a function called calcarea that calculates and returns the area of a circle; it is stored in a file called calcarea.m.

calcarea.m
function area = calcarea(rad)
% calcarea calculates the area of a circle
% Format of call: calcarea(radius)
% Returns the area

area = pi * rad * rad;
end

A radius of a circle is passed to the function to the input argument rad; the function calculates the area of this circle and stores it in the output argument area.

In the function header, we have the reserved word function, then the output argument area followed by the assignment operator =, then the name of the function (the same as the name of the file), and then the input argument rad, which is the radius.  As there is an output argument in the function header, somewhere in the body of the function we must put a value in this output argument.  This is how a value is returned from the function.  In this case, the function is simple and all we have to do is assign to the output argument area the value of the built-in constant pi multiplied by the square of the input argument rad.

The function can be displayed in the Command Window using the type command.

>> type calcarea

function area = calcarea(rad)
% calcarea calculates the area of a circle
% Format of call: calcarea(radius)
% Returns the area

area = pi * rad * rad;
end

The following is an example of a call to this function in which the value returned is stored in the default variable ans:

>> calcarea(4)
ans =
50.2655











Functions that return more than one value

The general form of a function definition for a function that calculates and returns more than one value looks like this:

functionname.m
function [output arguments] = functionname(input arguments)
% Comment describing the function
% Format of function call

Statements here; these must include putting values in all of the output arguments listed in the header

end

In the vector of output arguments, the output argument names are by convention separated by commas.


Choosing New, then Function brings up a template in the Editor that can then be filled in.  If this is not desired, it may be easier to start with New Script.

For example, here is a function that calculates two values, both the area and the circumference of a circle; this is stored in a file called areacirc.m:

areacirc.m
function [area, circum] = areacirc(rad)
% areacirc returns the area and
% the circumference of a circle
% Format: areacirc(radius)

area = pi * rad .* rad;
circum = 2 * pi * rad;
end

As this function is calculating two values, there are two output arguments in the function header (area and circum), which are placed in square brackets [  ].  Therefore, somewhere in the body of the function, values have to be stored in both.

As the function is returning two values, it is important to capture and store these values in separate variables when the function is called.  In this case, the first value returned, the area of the circle, is stored in a variable a and the second value returned is stored in a variable c:

>> [a, c] = areacirc(4)
a =
50.2655
c =
25.1327

If this is not done, only the first value returned is retained - in this case, the area:

>> disp(areacirc(4))
50.2655


The help function shows the comment listed under the function header:

>> help areacirc
This function calculates the area and
the circumference of a circle
Format: areacirc(radius)



Functions that do not return

The general form of a function definition for a function that does not return any values looks like this:

functionname.m
function functionname(input arguments)
% Comment describing the function

Statements here
end

Note what is missing in the function header: there are no output arguments and no assignment operator.

For example, the following function just prints the two arguments, numbers, passed to it in a sentence format:

printem.m
function printem(a,b)
% printem prints two numbers in a sentence format
% Format: printem(num1, num2)

fprintf('The first number is %.1f and the second is %.1f\n',a,b)
end

As this function performs no calculations, there are no output arguments in the function header and no assignment operator (=).  An example of a call to the printem function is:

>> printem(3.3, 2)
The first number is 3.3 and the second is 2.0

Note that as the function does not return a value, it cannot be called from an assignment statement.  Any attempt to do this would result in an error, such as the following:

>> x = printem(3, 5)  % Error!!
Error using printem
Too many output arguments.

We can therefore think of the call to a function that does not return values as a statement by itself, in that the function call cannot be imbedded in another statement such as an assignment statement or a statement that prints.














## Tutorials/The Basics
### Numbers and Calculations
```Shell
q)4*5
20
q)2+8+9 / This is a comment and is ignored.
19
q)5*1+2
15
```
> There is no order of operations in q, it simply executes from right to left (or left of right).  
> So 5\*1+2 <==> 5*(1+2).  
> We can enforce order of operation by using parentheses, however the more you can take advantage of the right-to-left evaluation, the more efficient your code will be. 

```Shell
q)(5*1)+2
7
q)2+5*1 / more efficient code uses less parentheses
7
```
### Variables
```Shell
q)x:5           / define x as a number (an atom, meaning a single item)
q)y:1 2 3       / define y as a list containing 1, 2, 3
q)x+y           / add x and y
6 7 8
q)x, y          / join x and y using comma
5 1 2 3
q)z:4 5 6 7     / define z as a list containing 4, 5, 6, 7
q)y+z           
'length
```
The last line is an error message:  
> You can add atoms to atoms, and atoms to lists, but you want to add lists to lists, they've got to be the same length.
```
q)count y
3
q)count z
4
```

### Datatypes
- Datatypes  
*type* returns the number corresponding to the input's datatype. the primitive datatypes table [http://code.kx.com/wiki/Reference/Datatypes](http://code.kx.com/wiki/Reference/Datatypes)
```Shell
q)type 5
-7h
q)type 1 2 3h
5h
q)type 5i
-6h
```
> The sign (-/+) indicates whether the input is an atom or a list: atoms have a negative type, whereas lists have a positive type.  
> The number (7/5/6) indicates the data type according to the primitive datatypes table.(7 is a long integer - the default integer data type, 5 is a short int, and 6 is int.  
> The character (h) is there simply because the output from type is itself a short.  

- Strings and Symbols 
> Text in kdb+/q is stored as either a string or a symbol.  
> A string is a list of characters, defined using a pair of quotation marks".  
> A symbol is an atomic datatype, defined using a single backtick`  

```Shell
q)mychar:"j"
q)mystring:"johnsmith"
q)type mychar
-10h
q)count mychar
1
q)type mystring
10h
q)count mystring
9
```
```Shell
q)mysymbol:`johnsmith
q)type mysymbol
-11h
q)count mysymbol
1
q)mysymbollist:`john`smith
q)count mysymbollist
2
```
> A symbol atom can contain any number of characters, whereas a string is really a list of chars. 
> Use symbols for repetitive lists & strings for mostly unique ones. 

- Temporal Datatypes
Datatypes 12-19 are all temporal: e.g. time, timestamp, date. 
```Shell
q)type 2016.03.16
-14h
q)type 2016.03.12 2016.10.21 1970.01.01
14h
```
```
q)2016.03.16+4
2016.03.20
q)22:11:59+2
22:12:01
q)22:11:59.345+2
22:11:59.347
```

- Casting between Datatypes
```Shell
q)string `johnsmith           / symbol to string
"johnsmith"
q)string 28                   / long to string
"28"
q)`int$3.14159                / float to integer
3i
q)`$"Hello"                   / string to symbol
`Hello
q)`int$"28"                   / string to integer: returns the ASCII code for each character
50 56i
```

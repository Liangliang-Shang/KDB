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
> A string is a list of characters, defined using a pair of quotation marks\".  
> A symbol is an atomic datatype, defined using a single backtick\`    

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

### Lists  
```Shell
q)a:1 2 3
q)b:7 8 9
q)symlist:`john`katie`david
q)charlist:"hello"
q)a+b
8 10 12
q)c:a,b                   // join
q)c
1 2 3 7 8 9
q)first symlist
`john
q)-2#c
8 9
q)5#a
1 2 3 1 2
```

- Single element lists  
```Shell
q)1#c
,1
q)type 1#c
7h
q)type first 1#c
-7h
q)enlist 5        // create a single element list
,5
```
- Indexing
```Shell
q)list:"helloworld"
q)list[0]
"h"
q)list[1 2 3]
"ell"
q)list 0 1 7 9
"herd"
```
- Search and Comparison
```Shell
q)p:12 8 10 1 9 11 5 6 1 5 4 13 9 2 7 0 17 14 9 18
q)p?9
4
q)p=9
00001000000010000010b
q)where p=9
4 12 18
q)p where p > 9
12 10 11 13 17 14 18
```
- Mixed Lists
```
q)mixedlist:("hey";1;`sym;1 2 3)
q)mixedlist
"hey"
1
`sym
1 2 3
q)type mixedlist
0h
q)type each mixedlist
10 -7 -11 7h
q)count each mixedlist
3 1 1 3
```
```Shell
q)mixedlist[0 3;1]
"e"
2
```
### Functions  
> q recognize up to 3 implicit parameters(x, y, z), but can declare up to 8 parameter names.    

> the square bracket/semicolon syntax for both passing in multiple inputs and declaring parameters.  

> statements are separated by ';'  

```Shell
q)til 5
0 1 2 3 4
q)sum 1 5 7 24
37
q){x+y+z}[1;2;3]    / 3 implicit parameters
6
q){[a;b]b+a*a}[3;5] / 3;5 two explicit parameters passing into a;b  
14
q)myfunc:{temp:x+y;temp*x*y}
q)myfunc[1;2]
6
q)temp              / temp is local in myfunc, not available      
'temp
```

### Dictionaries
> A dictionary is a mapiing between two lists: keys and values;   
> Syntax: \<keylist\>!\<valuelist\>      

```Shell
q)populations:`Texas`Florida`NewYork`Illinois`California!(26448193 19552860 26448193 12882135 38332521)
q)populations
Texas     | 26448193
Florida   | 19552860
NewYork   | 26448193
Illinois  | 12882135
California| 38332521
q)`a`b`c!1 2    / key list and value list must be the same length
'length
q)type populations  / the type of a dictionary is always 99h  
99h
q)populations[`Texas]
26448193
q)populations[`Texas`California]
26448193 38332521
q)populations`Texas`California
26448193 38332521
q)populations?38332521
`California
q)where populations = 26448193
`Texas`NewYork
q)where populations >= 26448193
`Texas`NewYork`California
q)key populations
`Texas`Florida`NewYork`Illinois`California
q)value populations
26448193 19552860 26448193 12882135 38332521
```

### Tables
- flip a dictionary to get a table
```Shell
q)mydict:`abc`def`ghi!(1 2 3;4 5 6;7 8 9)     / values are lists, all of the same length
q)mydict
abc| 1 2 3
def| 4 5 6
ghi| 7 8 9
q)flip mydict                                 / flip the dictionary to get a table
abc def ghi
-----------
1   4   7  
2   5   8  
3   6   9  
```
- define a table directly    
> defined within parentheses with columns separated by a semicolon ";".    
> empty square brackets at the begining means the table is unkeyed, and it has a type of 98h.    
> while a keyed table defined some of the columns within the square brackets, and its type is 99h    
```Shell
q)family:([]name:`John`Mary`David;age:52 49 18;hair:`brown`black`blonde;eyes:`blue`brown`blue)
q)family
name  age hair   eyes 
----------------------
John  52  brown  blue 
Mary  49  black  brown
David 18  blonde blue 
q)type family
98h
q)keyedtab:([a:`f`y`i]b:3 4 5;c:6 7 8)
q)keyedtab        / the vertical line seperating the first column from the others, similar to dictionaries.
a| b c
-| ---
f| 3 6
y| 4 7
i| 5 8
q)type keyedtab
99h
```
```Shell
q)2!family                  / keys on the first 2 columns
name  age| hair   eyes 
---------| ------------
John  52 | brown  blue 
Mary  49 | black  brown
David 18 | blonde blue 
q)3!family                  / keys on the first 3 columns 
name  age hair  | eyes 
----------------| -----
John  52  brown | blue 
Mary  49  black | brown
David 18  blonde| blue 
q)`age`eyes xkey family     / specifies columns to key on 
age eyes | name  hair  
---------| ------------
52  blue | John  brown 
49  brown| Mary  black 
18  blue | David blonde
q)0!keyedtab                / unkey a keyed table
a b c
-----
f 3 6
y 4 7
i 5 8
q)() xkey keyedtab          / () is an empty list
a b c
-----
f 3 6
y 4 7
i 5 8
```
- Index tables
> unkeyed tables are like lists: rows are numbered starting with 0.    
```Shell
q)family 0 2            / multiple rows make a table. (A table is a list of dictionaries.)
name  age hair   eyes
---------------------
John  52  brown  blue
David 18  blonde blue
q)family 1              / a single row is returned as a dictionary
name| `Mary
age | 49
hair| `black
eyes| `brown
q)keyedtab `y           / keyed tables are dictionaries, and their rows are identified by keys instead of numbers.
b| 4
c| 7
q)family`eyes           / access the columns of an unkeyed table as if it were a dictionary
`blue`brown`blue
```
- Inserts and Upserts
```Shell
q)`family insert (`Jessica;13;`black;`blue)       / return the row indices that have been added to the table
,3
q)family
name    age hair   eyes 
------------------------
John    52  brown  blue 
Mary    49  black  brown
David   18  blonde blue 
Jessica 13  black  blue 
q)family[3]
name| `Jessica
age | 13
hair| `black
eyes| `blue
q)`family upsert (`Avery;30;`black;`green)        / return the name of the table modified
`family
q)family
name    age hair   eyes 
------------------------
John    52  brown  blue 
Mary    49  black  brown
David   18  blonde blue 
Jessica 13  black  blue 
Avery   30  black  green
q)`keyedtab insert (`p;10;20)       / successfully inserted, returned the index 
,3
q)`keyedtab insert (`i;11;12)       / Wrong, already has a row with key `i
'insert
q)`keyedtab upsert (`i;11;12)       / updated the row with the key `i and returned the table name
`keyedtab
q)`keyedtab upsert (`j;13;14)       / updated the row with the key `j and returned the table name
`keyedtab
q)keyedtab
a| b  c 
-| -----
f| 3  6 
y| 4  7 
i| 11 12
p| 10 20
j| 13 14
```
- Quries
> select *columns* from *table* where *condition*    
> select *columns* by *column* from *table* where *condition*    
> the by clause allows you to perform aggregations or group the results based on a particular column/columns   
```Shell
q)select from family where hair=`black
name    age hair  eyes 
-----------------------
Mary    49  black brown
Jessica 13  black blue 
Avery   30  black green
q)select name, hair from family where age>30
name hair 
----------
John brown
Mary black
q)select avg age by hair from family
hair  | age     
------| --------
black | 30.66667
blonde| 18      
brown | 52      
q)exec name from family where eyes=`blue          / return a list as only one column is specified
`John`David`Jessica
q)exec name, eyes from family where hair=`black   / return a dictionary (with column names as keys) as multiple columns are requested
name| Mary  Jessica Avery
eyes| brown blue    green
```

- Updates and Deletes
> return a table modified in some way    
```Shell
q)delete eyes from family
name    age hair  
------------------
John    52  brown 
Mary    49  black 
David   18  blonde
Jessica 13  black 
Avery   30  black 
q)update age:age+1 from family where name in `John`Mary
name    age hair   eyes 
------------------------
John    53  brown  blue 
Mary    50  black  brown
David   18  blonde blue 
Jessica 13  black  blue 
Avery   30  black  green
q)family                / the table family remains exactly the same, the update/delete statments have simply returned a result 
name    age hair   eyes 
------------------------
John    52  brown  blue 
Mary    49  black  brown
David   18  blonde blue 
Jessica 13  black  blue 
Avery   30  black  green
q)/ a backtick is added before the tablename, which is a reference to the table stored in memory, actually modify the table
q)update surname:`Quill from `family
`family
q)family
name    age hair   eyes  surname
--------------------------------
John    52  brown  blue  Quill  
Mary    49  black  brown Quill  
David   18  blonde blue  Quill  
Jessica 13  black  blue  Quill  
Avery   30  black  green Quill  
q)delete from `family where name in `David`Jessica
`family
q)family
name  age hair  eyes  surname
-----------------------------
John  52  brown blue  Quill  
Mary  49  black brown Quill  
Avery 30  black green Quill  
```
- Joins
> *table* lj *keyed-table*    
> *table* ij *keyed-table*    
```Shell
q)students:([]id:140 265 204 212 367 197 329 242;class:`green`blue`green`orange`green`blue`green`gren)
q)students
id  class 
----------
140 green 
265 blue  
204 green 
212 orange
367 green 
197 blue  
329 green 
242 gren  
q)mentors:([]class:`green`blue`violet;mentor_name:("Julia Johnson";"Teddy Rowles";"Gerald Carlier"))
q)mentors
class  mentor_name     
-----------------------
green  "Julia Johnson" 
blue   "Teddy Rowles"  
violet "Gerald Carlier"
q)mentors,mentors
class  mentor_name     
-----------------------
green  "Julia Johnson" 
blue   "Teddy Rowles"  
violet "Gerald Carlier"
green  "Julia Johnson" 
blue   "Teddy Rowles"  
violet "Gerald Carlier"
q)mentors,students
'mismatch
q)students lj 1!mentors
id  class  mentor_name    
--------------------------
140 green  "Julia Johnson"
265 blue   "Teddy Rowles" 
204 green  "Julia Johnson"
212 orange ""             
367 green  "Julia Johnson"
197 blue   "Teddy Rowles" 
329 green  "Julia Johnson"
242 gren   ""             
q)students ij 1!mentors
id  class mentor_name    
-------------------------
140 green "Julia Johnson"
265 blue  "Teddy Rowles" 
204 green "Julia Johnson"
367 green "Julia Johnson"
197 blue  "Teddy Rowles" 
329 green "Julia Johnson"
q)students uj mentors
id  class  mentor_name     
---------------------------
140 green  ""              
265 blue   ""              
204 green  ""              
212 orange ""              
367 green  ""              
197 blue   ""              
329 green  ""              
242 gren   ""              
    green  "Julia Johnson" 
    blue   "Teddy Rowles"  
    violet "Gerald Carlier"
```

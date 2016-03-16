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

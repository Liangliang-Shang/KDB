## DollarSign  
1. cond  
2. x$y  
  2.1 cast  
  2.2 tok  
  2.3 enum  
  2.4 pad  
  2.5 product  
```Shell
q)$[0b;`true;`false]
`false
q)$[1b;`true;`false]
`true
```  
> $[q;a;$[r;b;c]] <==> $[q;a;r;b;c]  
> Only the first argument is guarentedd to be evaluated.  

```Shell
q){$[x>0;1;x<0;-1;0]}'[0 3 -9]
0 1 -1
```

```Shell
q)"I"$"28"
28i
q)(`int;"i";6h)$10
10 10 10i
q)1h$1 0 2
101b
q)`year`dd`dd`mm`hh`uu`ss$2015.10.28D03:55:58
2015 28 28 10 3 55 58i
q)flip{(x;.Q.t x;key'[x$\:()])}5h$where" "<>20#.Q.t
1h  "b" `boolean  
2h  "g" `guid     
4h  "x" `byte     
5h  "h" `short    
6h  "i" `int      
7h  "j" `long     
8h  "e" `real     
9h  "f" `float    
10h "c" `char     
11h "s" `symbol   
12h "p" `timestamp
13h "m" `month    
14h "d" `date     
15h "z" `datetime 
16h "n" `timespan 
17h "u" `minute   
18h "v" `second   
19h "t" `time     
```

```Shell
q)"D"$"2000-12-12"
2000.12.12
q)"U"$"12:13:14"
12:13
q)"T"$"123456789"
12:34:56.789
q)"P"$"2015-12-29D03:55:58.6542"
2015.12.29D03:55:58.654200000
q)flip{(neg x;upper .Q.t x;key'[x$\:()])}5h$where" "<>20#.Q.t
-1h  "B" `boolean  
-2h  "G" `guid     
-4h  "X" `byte     
-5h  "H" `short    
-6h  "I" `int      
-7h  "J" `long     
-8h  "E" `real     
-9h  "F" `float    
-10h "C" `char     
-11h "S" `symbol   
-12h "P" `timestamp
-13h "M" `month    
-14h "D" `date     
-15h "Z" `datetime 
-16h "N" `timespan 
-17h "U" `minute   
-18h "V" `second   
-19h "T" `time     
```  

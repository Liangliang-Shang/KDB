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
```Shell
q){$[x>0;1;x<0;-1;0]}'[0 3 -9]
0 1 -1
```

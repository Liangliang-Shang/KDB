# Abridged Kdb+ Database Manual
Arthur Whitney  
2006.10.13  
- Summary  
Kdb+ is an RDBMS and a general purpose programming language.  
The realtime OLTP+OLAP part of the database is generally in memory with an optional update log.  
No limit to the size of the OLAP historical database on disk.  
```Shell
q)trade:([]time:`time$();sym:`symbol$();price:`float$();size:`int$())
q)`trade insert(12:34:56.789;`xx;93.5;300)
,0
q)select sum size by sym from trade
sym| size
---| ----
xx | 300 
```  

- Install  
> Refer to [README.md](https://github.com/Lynn-Shang/KDB)  

- Server
```Shell
$q [f] [-p p] [-s s] [-t t] [-T T] [-o o] [-u u] [-w w] [-r r] [-l]
 f load script (*.q), file or directory                            
-p port kdbc(/jdbc/odbc) http(html xml txt csv)                    
-s slaves for parallel execution                                   
-t timer milliseconds                                              
-T timeout seconds                                                 
-o offset hours(from GMT: affects .z.Z)                            
-u usr:pwd file (-U allows file operations)                        
-w workspace MB limit                                              
-r replicate from :host:port                                       
-l log updates to filesystem (-L sync)                             
-z [0] "D"$ uses mm/dd/yyyy or dd/mm/yyyy
-P [7] printdigits(0:all)                
-W [2] week offset(0:sat)                
```
- Datatypes  
> There must be no spaces in symbol lists  
```Shell
q)symlist:`a`b`c
q)symlist
`a`b`c
```
- Insert and Upsert  
*`t insert ...* will check primary key violations.  
*`t upsert ... (also t,:...)* is insert for tables and upsert (update existing and insert new) for keyed tables.  

- Select and Update  
In general:  
> select [a] [by b] from t [where c]  
> update [a] [by b] from t [where c]  

- Table Arithmetic
```Shell
q)t:([x:`a`b]y:2 3)
q)u:([x:`b`c]y:4 5)
q)t+u
x| y
-| -
a| 2
b| 7
c| 5
```


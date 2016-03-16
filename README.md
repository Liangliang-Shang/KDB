# KDB-
KDB+/Q

## Installation  
  1. ```sudo apt-get install libc6-i386```
  2. ```sudo apt-get install rlwrap```
  2. Download linux.zip from [https://kx.com/software-download.php](https://kx.com/software-download.php)
  3. Unzip linux.zip and move the extracted q directory to /home/lshang/devel
  4. ```export QHOME="/home/lshang/devel/q"```
  5. ```alias q='rlwrap -c -r $QHOME/l32/q```
  6. type q in the terminal: 
```bash
20160316 21:10:44 lshang@elemos:/home/lshang/devel 
$ q
KDB+ 3.3 2016.03.08 Copyright (C) 1993-2016 Kx Systems
l32/ 8()core 3901MB lshang elemos 127.0.1.1 NONEXPIRE  

Welcome to kdb+ 32bit edition
For support please see http://groups.google.com/d/forum/personal-kdbplus
Tutorials can be found at http://code.kx.com/wiki/Tutorials
To exit, type \\
To remove this startup msg, edit q.q
q)
```
